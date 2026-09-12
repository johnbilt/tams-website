---
layout: post
title: TAMS is becoming a Linux Foundation project
date: 2026-09-11
image: /images/blog_images/2026-tams-linux-foundation-logo.png
hero_image: /images/blog_images/2026-tams-linux-foundation-header.png
hero_height: is-small
hero_darken: true
author: Sam Mesterton-Gibbons
tags:
    - Governance
    - TSC
    - Open Source
    - BBC
    - Linux Foundation
---

In early 2018, BBC R&D published our initial thinking on [cloud-fit media production](https://www.bbc.co.uk/rd/blog/2018-03-cloud-video-production-stream-file-frame), which would lead to the open-source [Time-addressable Media Stores (TAMS) API](https://github.com/bbc/tams) specification and the transformation of fast-turnaround workflows. That specification is now in use across multiple media organisations (including the BBC), and available in a growing list of commercial and open-source products. Now we're excited to share the next chapter, as TAMS transitions to be a Linux Foundation project, owned and managed by the community.

Far from being the end of this journey, BBC R&D plan to keep evolving and developing TAMS, integrating it into the BBC's workflows and exploring new areas of work around how media and data can work together. However, it became clear after we released TAMS as an open-source specification that it was too important to too many people to remain under the exclusive control of BBC R&D. As a result, we worked with some of the [TAMS community](https://tams.org/2026/04/15/new-tsc-members) to figure out how to ensure the longevity and sustainability of TAMS as a specification and an open ecosystem.

This post will explore how we got here, what that means for TAMS and software-based media supply chains, and what comes next.

## How we got here

TAMS started out to answer the question, "How do we make media production more cloud-fit?". We initially explored whether that was even possible, and wrote up [our findings](https://www.bbc.co.uk/rd/blog/2018-05-storing-frames-in-the-cloud-part-2-getting-them-back-out-again) around object store performance, latency, and architecture. We went on to build a suite of cloud services to demonstrate our ideas in reality, used to great effect as the media backend for [The Watches](https://www.bbc.co.uk/rd/blog/2022-04-video-cloud-media-store-ingest-service).

Following this success, BBC R&D started considering how to move this technology out of the lab and into production. For IBC 2023, we [released the TAMS specification as an open-source project](https://www.bbc.co.uk/rd/articles/2024-09-time-addressable-media-store-cloud-production) and shared it with various industry partners. AWS formed the Cloud Native Agile Production (CNAP) initiative and brought several of their partners together to build interoperable TAMS [demos at IBC 2024](https://aws.amazon.com/blogs/media/aws-bbc-adobe-and-others-introduce-open-source-framework-for-fast-turnaround-media-workflows-at-ibc-2024/). TAMS continued to grow through 2025, leading to a [Broadcast Tech Innovation Award](https://www.broadcastnow.co.uk/tech/broadcast-tech-innovation-awards-2025-the-winners-and-judges-comments/5211419.article) for Best Innovative Use of Cloud and an IABM Industry Partnership Award for next-generation news distribution [demonstrated at IBC 2025](https://tams.org/2025/09/12/IBC-demo-videos).

It became clear to us that TAMS should be owned by the community, and we [set out plans](https://tams.org/2026/01/28/tams-governance) to transition to an open governance model, with [four goals](https://github.com/bbc/tams/blob/main/GOVERNANCE.md#goals) for a future approach to governance of TAMS:

1. Ensure the longevity and stability of the TAMS API specification and associated ecosystem.
2. Ensure that TAMS as a technology is owned by the community, rather than controlled by any one organisation.
3. Create space to grow the community.
4. Provide a framework to set the project direction and facilitate technical decision making.

BBC R&D and AWS established a Technical Steering Committee (TSC) and recruited additional members from the TAMS community. We evaluated a range of potential models and host organisations, including industry groups, standardisation organisations, and open-source foundations. We carried out background research and drew on the experience of R&D colleagues working on [MXL](https://github.com/dmf-mxl/mxl) and [C2PA](https://c2pa.org/). Several of the TAMS community also kindly introduced us to teams at the Linux Foundation and Academy Software Foundation, and we're grateful for their help in setting up discussions.

Following discussions among the TAMS TSC, we concluded that the Linux Foundation's Community Project model offered the best balance of flexibility for TAMS to continue to grow in future without significant overhead or burden on our existing community.

We’ve published the full analysis and our conclusions as a TAMS Architecture Decision Record (ADR) [on GitHub](https://github.com/bbc/tams/blob/main/docs/adr/0051-host-organisation-for-tams.md).

## What does this mean for the TAMS community?

In practice very little will change: TAMS remains an open-source project licenced under Apache 2.0, and the Supply Chain and Software Foundations team in BBC R&D will continue to develop the specification and supporting ecosystem.

A new Linux Foundation project is being set up, with the existing Technical Steering Committee continuing to steer and manage the project. As part of that, the repository will move out of the BBC's GitHub organisation (but we'll set up a redirect), and the new project will also take ownership of the TAMS domains, website and branding.

As with all Linux Foundation projects, it is a neutral home for the code, specifications, and assets of TAMS. Contributors are free to participate regardless of employer or affiliation, and the lightweight "Community Project" model is very similar to the approach used today, backed by a well-established legal and governance framework. For now, we've also chosen not to use one of the Linux Foundation funding models, unless and until it becomes clear to the TSC that we should. TAMS will always welcome contributions, and the specification will always be free and open: this is a foundational tenet of Linux Foundation projects.

## Where do we go next?

We're still hard at work supporting the TAMS community and helping to roll it out within the BBC's own operations. To help with that, we're developing a test and validation suite to explore whether TAMS servers, readers, and writers correctly implement the specification (which we'll be open sourcing shortly). We're also exploring what "TAMS for data" might look like, and how we can take advantage of the strong identity and write-once, use-many model of TAMS in novel workflows: more on that shortly, too.

When we [announced the move to open governance](https://tams.org/2026/01/28/tams-governance) at the start of 2026 we said that the final phase was to "balance" the TSC with no organisation controlling more than one vote. We'll set out plans to recruit new members and vacate two of the BBC's three seats in due course.

Overall, TAMS is one part of a wider transformation: towards granting media organisations the agility to adapt and respond to new opportunities and the needs of their audiences. It does that by fostering an open ecosystem, built on interoperable foundations, defined as software. An ecosystem moving at the speed our industry, and our audiences, demand.

_Originally published at https://www.bbc.co.uk/rd/articles/2026-09-tams-open-governance-linux-foundation._

_The Linux Foundation and The Linux Foundation logo design are registered trademarks of The Linux Foundation. Linux is a registered trademark of Linus Torvalds_