---
layout: radial-infographic
permalink: /about/use-cases-infographic/
kicker: About
title: TAMS Use Cases
subtitle: What can you do with a TAMS store?
hero_image: /images/resources_background.png
hub_icon: fa-database
hub_title: TAMS Store
cards:
  - title: Live Ingest
    icon: fa-broadcast-tower
    summary: Capture live feeds directly into the store as growing timelines, available for immediate use.
    detail: |
      **Live Ingest** writes incoming live feeds (cameras, satellite, IP streams) into the TAMS store in real time as short media chunks.

      **How it works with TAMS:**
      - Media is segmented into short chunks (typically 1-6 seconds) and uploaded via pre-signed URLs
      - Each chunk is registered as a Segment on a growing Flow timeline
      - Content is available for downstream use (editing, playout) as soon as each Segment is registered — no need to wait for the recording to finish
      - Multiple ingest points can write to the same store simultaneously
      - Different quality levels (proxy, mezzanine, full-res) can be ingested as separate Flows under the same Source

      **Benefits:** Immediate availability, parallel access, no file locking, natural scalability for multi-camera productions.

  - title: Edit While Record
    icon: fa-cut
    summary: Start editing content while it's still being recorded, with no file locks or delays.
    detail: |
      **Edit While Record** enables editors to begin working with content the moment it starts arriving in the store.

      **How it works with TAMS:**
      - As new Segments are registered on a growing timeline, editors see the timeline extend in real time
      - No file locks — the ingest system writes Segments while editors read them simultaneously
      - Edit decisions reference Segments by time range, so they remain valid as the recording grows
      - Multiple editors can work on the same Source concurrently without conflict
      - Proxy Flows give lightweight access while full-resolution Flows remain available for conform

      **Benefits:** Dramatically reduces time-to-air for live events, news, and sports. Editorial decisions can begin seconds after content is captured.

  - title: Edit by Reference
    icon: fa-link
    summary: Create new versions by referencing existing media — no copying, no duplication.
    detail: |
      **Edit by Reference** allows new programmes or sequences to be assembled by pointing to existing media Objects rather than copying them.

      **How it works with TAMS:**
      - A new Flow is created for the edit output
      - Segments on the new Flow reference the same Object IDs as the source material
      - Offsets and partial ranges allow using only a portion of an Object
      - The store tracks all references automatically — nothing is orphaned
      - Multiple edit versions can coexist referencing the same underlying media
      - Conform to full-resolution is a metadata operation, not a media copy

      **Benefits:** Instant edit assembly, minimal storage duplication, fast multi-version workflows, efficient use of storage capacity.

  - title: Multi-Resolution
    icon: fa-layer-group
    summary: Store multiple quality levels of the same content, from proxy to full resolution.
    detail: |
      **Multi-Resolution** workflows store the same content at different quality levels, all linked under a single Source identity.

      **How it works with TAMS:**
      - Each resolution is a separate Flow (e.g. proxy, HD, UHD) sharing the same Source ID
      - Timelines align across Flows — a time range on the proxy maps to the same moment on the full-res
      - Editors work on lightweight proxy Flows, then conform switches to the full-resolution Flow
      - Transcoding services can watch for new content and automatically generate additional Flows
      - Quality levels can be added or removed independently without affecting other Flows

      **Benefits:** Fast editorial with proxies, lossless conform, flexible storage tiering, independent lifecycle per resolution.

  - title: Playout & Distribution
    icon: fa-play-circle
    summary: Read from the store for playout, streaming, or packaging — using time-based queries.
    detail: |
      **Playout & Distribution** uses the TAMS store as the source for live or file-based output to viewers.

      **How it works with TAMS:**
      - Playout systems query the store for Segments within a time range
      - Pre-signed URLs allow direct media download from object storage at scale
      - Growing timelines support live pass-through — playout follows the ingest in near real-time
      - Multi-essence Flows provide the complete programme (video + audio) as a single reference
      - Time-based access means playout can jump to any point on the timeline without scanning

      **Benefits:** Scalable read access, no single point of failure, time-accurate retrieval, supports both live and on-demand delivery.

  - title: AI & Metadata Enrichment
    icon: fa-robot
    summary: Run AI and analysis tools against content in the store, writing metadata back as tags.
    detail: |
      **AI & Metadata Enrichment** uses automated tools to analyse content in the store and enrich it with searchable metadata.

      **How it works with TAMS:**
      - AI services read media directly from the store via pre-signed URLs
      - Analysis results (speech-to-text, face detection, scene classification) are written back as tags on Sources or Flows
      - Time-coded annotations can reference specific time ranges
      - Multiple AI services can process the same content in parallel
      - Enrichment can happen on ingest (real-time) or as batch processing later
      - Tags enable downstream discovery and automated workflow triggers

      **Benefits:** Content becomes searchable immediately, workflows can be triggered by metadata, no manual logging required.

  - title: Archive & Preservation
    icon: fa-archive
    summary: Long-term storage with full metadata, timeline integrity, and retrieval by time.
    detail: |
      **Archive & Preservation** uses the TAMS store for long-term content retention with rich metadata and time-based retrieval.

      **How it works with TAMS:**
      - Content retains its full timeline structure and metadata in the archive
      - Storage tiering (hot/warm/cold) can be applied per Flow or per time range
      - Retrieval is time-based — pull specific moments without restoring entire programmes
      - Tags and Source metadata make archived content discoverable
      - Object re-use tracking ensures referenced media is never incorrectly deleted
      - The API abstraction means archive storage can move between backends transparently

      **Benefits:** Granular retrieval, no stranded assets, storage cost optimisation, future-proof access via API.

  - title: Multi-Site & Cloud
    icon: fa-cloud
    summary: Distribute content across locations and cloud regions with a consistent API.
    detail: |
      **Multi-Site & Cloud** workflows span multiple physical locations or cloud regions while presenting a unified content view.

      **How it works with TAMS:**
      - Each location can run its own TAMS store instance
      - Sources and Flows can be replicated or federated across stores
      - The API is location-agnostic — clients don't need to know where media physically resides
      - Regional ingest writes locally, with metadata and/or media synced to other sites
      - Edit-by-reference works across sites when media is accessible via the same Object IDs
      - Disaster recovery and redundancy are built into the distributed model

      **Benefits:** Local performance, global access, resilient architecture, cloud-native scalability.

  - title: Collaborative Workflows
    icon: fa-users
    summary: Multiple users and systems work on the same content simultaneously without conflicts.
    detail: |
      **Collaborative Workflows** enable teams to work together on content without file locks, version conflicts, or sequential handoffs.

      **How it works with TAMS:**
      - The store allows concurrent read and write access to the same Sources and Flows
      - Each editor or system creates their own Flows for edit outputs, referencing shared media
      - No check-in/check-out model — access is always available
      - Tags and metadata updates are non-destructive and additive
      - Webhooks and events can notify collaborators of changes in real time
      - Different roles (journalist, editor, QC) can work in parallel on different aspects of the same content

      **Benefits:** Faster team workflows, no bottlenecks, parallel rather than sequential processing, full audit trail.
---

## Use Cases

A TAMS store sits at the centre of your media workflow. Click any use case to explore how it interacts with the store.
