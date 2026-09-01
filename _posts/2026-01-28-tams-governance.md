---
layout: post
title: Moving TAMS towards Open Governance
hero_darken: true
image: /images/blog_images/2026_governance_blog_header.jpg
hero_image: /images/blog_images/2026_governance_blog_header.jpg
hero_height: is-small
hero_darken: true
author: Sam Mesterton-Gibbons
tags:
    - Governance
    - TSC
    - Open Source
    - BBC
---

In 2023 BBC Research & Development made the first open source release of TAMS at [https://github.com/bbc/tams/](https://github.com/bbc/tams/), and has owned the repository and co-ordinated contributions ever since. 
However as more systems, solutions and products are built on TAMS, it is clear that it should be owned by the community, and a more formal process put in place to govern the project and ensure longevity and stability.

This blog post will describe our plan to ensure we make the right decisions for the future of TAMS, continuing the BBC's involvement while giving the community more control and ownership over the project. 
We're keen to take our time, and to do this right, so we're going to proceed in phases with a period of research and evaluation.
We're planning to move to an open governance model, under an existing open source organisation such as the [Linux Foundation](https://www.aswf.io/) or projects like the [Academy Software Foundation](https://www.aswf.io/) or the [Alliance for Open Media](https://aomedia.org/).

Fundamentally the TAMS API is a specification for writing interoperable software, and for that reason we feel a software-oriented approach is more appropriate than a more formal standardisation route through SMPTE or similar. 
The specification will continue to grow and change as the community iterates on what it needs, applying standard software versioning techniques to rapidly bring new capabilities without unduly breaking existing implementations. 
We also value building an open ecosystem, without locking into an industry member or geographical organisation, which pushes us towards the approach of other industry projects on a similar journey (notably [MXL](https://github.com/dmf-mxl/mxl)).

Regarding the specific details of open governance, it is not yet clear precisely which project to align to, so initially in a "Setup Period" a Technical Steering Committee (TSC) will be formed of existing contributors (drawn from the BBC, AWS and others), who will be charged with evaluating options and making a decision, which will be shared with the community. 
Following this (in the “Transition Period”) the TSC will implement this decision, moving the TAMS repository away from the BBC GitHub Organisation, and putting in place remaining parts of the formal governance framework. 
Part of this process will see the TSC being rebalanced - no organisation will control more than one vote, with those that do in the "Setup Period" relinquishing seats, and new members being found.

For the BBC, TAMS provides the opportunity to build a more diverse media supply chain out of interoperable components which we take from industry vendors, without having to rely on monolithic systems and complex integrations. 
This enables us to execute on our technology strategy of "SaaS first", and make our supply chain more flexible and agile to the needs of the future.

We started the "Cloudfit Production" project (which would become TAMS) back in 2018 with the goal of working out how to build fully cloud-native media production workflows. 
We hypothesised a central media store of small segments, processed independently without critical paths through the system. 
We developed a number of services and demonstrations, showing ingest and output of streams (including uncompressed video) and files, along with experimental designs for scaleable processing. 
Our work with [The Watches](https://www.bbc.co.uk/rd/articles/2022-04-video-cloud-media-store-ingest-service) gave the project focus and showed the
value of it in real production uses cases. Eventually it became clear that the value
was in the interface (rather than the implementation), and we were able to open
source the TAMS API ahead of IBC 2023. Shortly after that AWS got involved and
helped pull together the initial set of partners and vendors to produce the successful
demo at IBC 2024, and the demo at IBC 2025, winner of the IABM Industry
Partnership Award and Broadcast Tech Innovation Award for Best Innovative Use of
Cloud.

Going forward, the BBC remains fully committed to TAMS and is actively working to
deploy it. The team in BBC R&D will continue to explore new areas of research and
interest, while also shepherding TAMS through the governance process and
continue to research, develop and advise going forward. The Royal Charter instructs
the BBC to “maintain a leading role in research and development…and share, as far
as is reasonable, its research and development knowledge and technologies”, and
TAMS is one example of doing so, providing benefit for both the BBC, and the wider
media industry.

In the near future the TSC will form and start arranging meetings to work through
the governance process. See
[https://github.com/bbc/tams/blob/main/GOVERNANCE.md](https://github.com/bbc/tams/blob/main/GOVERNANCE.md) for more on the initial
direction and tasks.

TAMS succeeds on the strength of the community behind it, and suggestions on
governance and the future direction of the project are greatly appreciated: on Slack,
or directly to cloudfit-opensource@bbc.co.uk

