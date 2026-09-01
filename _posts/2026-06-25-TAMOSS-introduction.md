---
layout: post
date: 2026-06-25
title: TAMS is a Kubernetes-shaped problem
subtitle: Guest post from David O'Dwyer at LiveWyer 
image: /images/blog_images/2026-livewyer-blog-heading.png
hero_image: /images/blog_images/2026-livewyer-blog-heading.png
hero_height: is-small
hero_darken: true
title: "TAMS is a Kubernetes-shaped problem"
description: "TAMOSS is the LiveWyer open-source, Kubernetes-native implementation of the TAMS API: why a time-addressable media store is a Kubernetes-shaped problem, and how it was built."
author: David O'Dwyer
tags:
    - TAMOSS
    - Kubernetes
    - Operator
    - Cloud Native Media
    - Open Source
    - Guest Post

---

We welcome David O'Dwyer from [LiveWyer](https://livewyer.io/) to introduce TAMOSS and why a time-addressable media store is a Kubernetes-shaped problem, and how it was built.

---

# TAMS is a Kubernetes-shaped problem

## Introduction

TAMS is designed to run anywhere.

That's not me editorialising, it's in [the spec's own principles](https://github.com/bbc/tams): agnostic to clouds, codecs and containers, deployable on-premise and at the edge as happily as in a hyperscaler. It's one of my favourite things about it. But there's a long way between a spec that can run anywhere and software you can actually stand up on your own kit, and further still to something you'd trust in production.

TAMOSS is our first step down that road: an open-source, Kubernetes-native implementation of the TAMS API, built by LiveWyer and released under Apache 2.0. This post is about why TAMOSS is a big step toward enabling teams to have an instant TAMS test instance and towards a production TAMS implementation.

## The reference implementation got us here

Most people's first introduction to TAMS is through the [AWS reference implementation](https://github.com/awslabs/time-addressable-media-store). It's a serverless design with the API Gateway in front of Lambda functions, DynamoDB for the index, S3 for the media, with SQS, EventBridge and Cognito around the edges. And it's good. It teaches you the API, proves the model, and makes it clear in its README that it's meant for development rather than production. Which is exactly what a reference should be. Without it, TAMOSS wouldn't exist. It's how we, and I suspect most people in this ecosystem, learned the shape of the API.

What a reference deliberately leaves open is everything that comes after "it works". That is not for want of effort on AWS's part. They have done a lot to get TAMS in front of teams, and the serverless design is how most people first deploy the API. The limit is in the architecture itself: it is built around AWS primitives, so it runs well but it runs in one place.

How do you run a store somewhere that isn't AWS? On your own hardware, in a private cloud, at the edge, across the mix of places a real media operation actually lives? And how do you keep it running once it's there?

That's the part we picked up, and to us, it looked like a Kubernetes problem from day one.

## Why Kubernetes?

Strip TAMS down and you get a stateless HTTP API in front of two pluggable stores, a database for the timeline index and an object store for the media, plus a lifecycle around it all that has to stay correct as things change.

Read that back slowly. It's close to a textbook description of what Kubernetes operators exist to manage.

The API is stateless, so it wants to be a horizontally scalable `Deployment` behind a `Service`. The media plane is S3-compatible by design, which is about the most portable storage contract in computing: the same code runs against a hyperscaler bucket (a [RustFS](https://rustfs.com/) or [MinIO](https://min.io/) cluster in your own racks, or [Backblaze B2](https://www.backblaze.com/cloud-storage)). The metadata plane is a database, and running one on Kubernetes (or pointing at a managed one) is well-trodden ground. And the bit that usually gets hand-rolled, the ongoing job of assembling all this into a healthy system and keeping it that way, is literally what an operator does. You declare the state you want, and a controller works to make reality match.

Storage backends are a good example. Since version 7 of the spec, a single TAMS store can span multiple object stores. Model a backend as a custom resource, and that stops being bespoke integration work: you declare it, the platform wires it in. The spec's separation of concerns makes TAMS portable on paper. Kubernetes is what turns that into a store you can stand up on real infrastructure.

## What we built

TAMOSS installs as an operator-driven product. The operator, written in Go with [Kubebuilder](https://book.kubebuilder.io/) and [controller-runtime](https://github.com/kubernetes-sigs/controller-runtime), watches two custom resources, `Tamoss` and `StorageBackend`, and reconciles them into a running system: API, async worker, web UI, schema migrations, the Secrets they all need, ingress routing, and whichever backends you've selected. You describe the store you want, the operator builds it and keeps it built.

There are three profiles, all on the same path:

- `local-kind` brings everything up on a [Kind](https://kind.sigs.k8s.io/) cluster on your laptop, bundled database, object storage, auth and ingress included, so you can poke at a real store within minutes.
- `single-server` targets one node or a small self-managed cluster.
- `multi-server` is the production-shaped, replicated topology.

Same path everywhere, so what you learn on your laptop is what you run in your data centre. Locally, it's one command:

```bash
task kind:up PROFILE=local-kind
```

Every platform service is pluggable via the same declarative interface, which is how a single product reaches so many environments. Per service, TAMOSS provides it, or you bring your own:

```yaml
apiVersion: tamoss.livewyer.io/v1alpha1
kind: Tamoss
metadata:
  name: newsroom
  namespace: tams
spec:
  backends:
    db:
      providedBy: external      # or bundled, or cnpg (CloudNativePG)
    s3:
      providedBy: external      # or bundled, or rustfs-operator
  auth:
    providedBy: external        # external OIDC, or authentik-blueprints
```

The design decision I'm most pleased with is actually invisible from the outside: the API knows nothing about Kubernetes.

All the Kubernetes-specific work lives in the operator. The application just reads its configuration and a credentials file from a mounted Secret; the operator is what turns custom resources into those files and keeps them current. That's deliberate. It means the same store can run somewhere that isn't Kubernetes at all, as long as something supplies the same files, and we never have to teach the API about whatever platform it happens to be sitting on.

And because the goal is to operate TAMS, not just run it, the operator does day-2 work too. It reports readiness through status conditions and Events, corrects drift when something (or someone) fiddles with the resources it manages, and puts an admission webhook in front of destructive deletes, so nobody removes a store without confirming it with an explicit annotation.

We're early on this, and there's plenty still to do. But the direction matters to us: production-readiness as something the platform helps with, rather than a pile of runbooks.

## Building on open foundations

TAMS is where it is because the community has spent years making it an implementable [open standard](https://timeaddressablemediastore.org/), with the application notes, decision records and governance to match. Even picking up the [IABM Industry Partnership Award at IBC2025](https://timeaddressablemediastore.org/2025/12/01/broadcast-award.html). The foundations are robust, and we are pleased to add to them with TAMOSS.

But to be clear, TAMOSS is just one independent implementation among what should be many. More implementations were always the point; it's written into the spec's principles, and the team behind TAMS has been glad to see another one arrive.

Where we're looking next is the live plane. TAMS covers stored, time-addressable media. The EBU and NABA's [Dynamic Media Facility](https://tech.ebu.ch/groups/dmf) work includes [MXL, the Media eXchange Layer](https://tech.ebu.ch/dmf/mxl), a shared-memory data plane for moving media between live functions, container-friendly from the start. TAMS for the stored side, MXL for the live side, both as cloud-native workloads, and you can start to see a broadcast facility built the way we build everything else.

TAMOSS is open source and available now at [github.com/livewyer-ops/tamoss](https://github.com/livewyer-ops/tamoss). If you run media infrastructure and have wanted a TAMS store you can own end to end, then bring it up on your laptop. Kick the tyres, and tell us where it breaks.

---

Blog first published on the [LiveWyer website](https://livewyer.io/blog/tams-is-a-kubernetes-shaped-problem/)