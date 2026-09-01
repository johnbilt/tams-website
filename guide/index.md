---
layout: infographic
permalink: /guide/
kicker: Guide
title: Guide to Working With TAMS
subtitle: Understanding the building blocks
hero_image: /images/resources_background.png
cards:
  - title: Sources
    icon: fa-project-diagram
    summary: The primary point of discovery for content in TAMS — representing what the content is, independent of any particular format or resolution.
    detail: |
      A **Source** represents a piece of content at its most abstract level — it identifies *what* the content is, not how it's stored or encoded. Sources are the entry point for users and systems discovering content in the store.

      **Key points:**
      - Sources are the primary discovery mechanism — media workflows and applications should use Sources as their references to media (e.g. a MAM might reference an asset using the ID of a Source, in lieu of a file name)
      - Business logic is then applied to identify a suitable Flow representing that Source when operations need to be performed — for example, choosing between proxy-quality for an offline edit and full-quality for a render
      - Sources are identified by UUID and carry human-readable metadata: a **label** (short-form identifier) and **description** (additional context to help locate and identify content)
      - Multi-essence Sources collect related mono-essence Sources (e.g. combining a video Source with its audio Source) — this "muxed" version is what users are typically aware of
      - Sources are created implicitly when you create a Flow referencing them — there is one consistent route to Source creation
      - The Source data model deliberately does not contain a rich editorial metadata model — for complex metadata, use a MAM layer on top of TAMS
      - The data model is based on the AMWA NMOS MS-04 model and the JT-NM Reference Architecture, meaning the terminology will be familiar to anyone who has worked with live IP video

      **Example:** A news package called "Election Night Coverage" is a Source. It might have Flows for 1080p contribution quality, a 720p proxy, and a UHD master — all discoverable under the same Source identity. A journalist searches for the Source by label; the system selects the appropriate Flow based on the task at hand.

  - title: Flows
    icon: fa-stream
    summary: A specific technical rendition of a Source — holding the codec, resolution, frame rate, sample rate and other format-specific parameters.
    detail: |
      A **Flow** represents a specific technical rendition of a Source. While Sources represent *what* the content is, Flows represent *how* it is stored and encoded. Flows are the element you create when writing content into TAMS.

      **Key points:**
      - There are five types of Flow: **Video** (video-only segments), **Audio** (audio-only segments), **Data** (non-media segment types), **Images** (still images) and **Multi** (collecting mono-essence Flows together)
      - Each Flow references the Source to which it belongs — if the Source doesn't exist, the store creates it automatically, initially replicating the Flow's label and description
      - For content with multiple versions (e.g. HD and proxy), multiple Flows are created under the same Source — the content must be editorially identical, just with different technical characteristics
      - Multi-essence Flows collect mono-essence Flows together to represent a combined programme — they have no media stored directly against them
      - Each Flow has its own virtual, infinite timeline where Segments are registered
      - The API is format-agnostic: you can specify codec, container/wrapper, bit rate, frame rate, bit depth, sample rate and other parameters when creating a Flow
      - Creating mono-essence Flows first, then collecting them into a multi-essence Flow, is the standard creation sequence

      **Example:** A Source "Election Night Coverage" has: a 1080p50 H.264 video Flow, a 720p25 proxy video Flow, a 48kHz 24-bit PCM audio Flow, a 48kHz AAC audio Flow, and a multi-essence Flow collecting the HD video and PCM audio together.

  - title: Time Ranges
    icon: fa-arrows-alt-h
    summary: The temporal notation system that provides nanosecond-precision addressing of media on a Flow's timeline, using International Atomic Time (TAI).
    detail: |
      A **Time Range** defines a span of time on a Flow's timeline. Rather than using traditional SMPTE timecode, TAMS uses International Atomic Time (TAI) with nanosecond precision — the fundamental mechanism for addressing media by time.

      **Key points:**
      - Format: `[start:nanoseconds_end:nanoseconds)` — e.g. `[1694429247:0_1694429248:0)` is a 1-second timerange
      - Boundary markers: `[` or `]` means inclusive; `(` or `)` means exclusive
      - For continuous segments, the convention is inclusive start, exclusive end — e.g. `[0:0_10:0)` followed by `[10:0_20:0)` declares no gap between them
      - Special forms: `_` alone represents "eternity" (the entire timeline); `()` represents "never" (zero-length range); `[1694429247:0]` is an instantaneous timestamp (e.g. for images)
      - Overlapping segments on the same Flow are **not** allowed — the store will reject them. Gaps are permitted (e.g. camera not recording, or partial replication between stores)
      - Time ranges enable querying: you can request all segments within a given window, and the store returns those that partially or fully fall within it
      - The move away from SMPTE timecode eliminates midnight-crossing issues and supports recordings longer than 24 hours
      - For live feeds, encoders locked to PTP generate timing data, ensuring all feeds are time-referenced correctly relative to each other
      - Timelines can be populated in any order — enabling gap-filling after connection interruptions

      **Example:** `[5:0_45:0)` queries a Flow's timeline from 5 seconds (inclusive) to 45 seconds (exclusive). If the Flow has 10-second segments at `[0:0_10:0)`, `[10:0_20:0)`, `[20:0_30:0)`, `[30:0_40:0)`, `[40:0_50:0)`, the store returns all five segments as they each partially or fully overlap the query window.

  - title: Segments
    icon: fa-puzzle-piece
    summary: The bridge between a Flow's logical timeline and physical media — mapping a time range to a specific media Object in storage.
    detail: |
      A **Segment** maps a time range on a Flow's timeline to a specific media Object in storage. It is the link between the logical timeline and the actual media files.

      **Key points:**
      - Each Segment declares a timerange (where it sits on the Flow's timeline) and references an Object ID (the actual media file)
      - Segments are uploaded to object storage first, then registered against the appropriate Flow with their timing data
      - Once registered, a Segment's Object can be reused across multiple Flows — this is "edit by reference". New edits reference existing Objects without duplicating media
      - The store handles housekeeping: Objects used by multiple Segments are only deleted when no references remain
      - Segments are registered against mono-essence Flows only — multi-essence Flows have no direct Segments
      - Media files should be short, independently decodable chunks — for Long GOP codecs, segments should contain complete GOPs
      - When re-using an Object on a different timeline, `ts_offset` maps the media object's internal timeline to the Flow timeline. Partial usage of an Object is supported via `object_timerange`
      - The first registration of an Object against a Segment MUST be against the Flow for which storage was originally allocated (for security and lifecycle management)

      **Example:** An encoder produces 6-second chunks of H.264 video. Each chunk is uploaded to S3 via a pre-signed URL, then registered as a Segment: Object ID `abc123`, timerange `[120:0_126:0)`. Later, an editor creates a highlights reel that references the same Object at a different position on a new Flow's timeline — no media is copied.

  - title: Objects
    icon: fa-file
    summary: The physical media files — independently decodable chunks of video, audio or data stored in object storage and accessed via pre-signed URLs.
    detail: |
      An **Object** is the physical media file — the actual bytes of video, audio or data stored in object storage (e.g. S3). Objects are the atomic unit of media in TAMS.

      **Key points:**
      - Objects are stored in standard cloud object storage and accessed via pre-signed URLs provided by the TAMS API — no separate storage credentials are needed
      - The upload workflow: (1) request storage allocation from TAMS, (2) receive pre-signed URLs, (3) upload directly to object storage, (4) register the Object against a Flow by creating a Segment
      - Objects can be shared across multiple Flows and Segments — this is the basis of edit-by-reference and enables zero-copy content reuse
      - The store tracks Object reuse via reference counting — Objects are only deleted from storage when no Segments reference them
      - Objects now carry an `object_timerange` property describing the timerange of media contained within them, enabling precise partial-object usage
      - Objects are typically short media chunks (seconds to minutes) rather than entire programmes — this enables low-latency access and fine-grained reuse
      - Object Instances allow the same logical Object to exist in multiple storage backends (e.g. for redundancy or geographical distribution)
      - If content is bit-identical, it should use the same Object ID — duplication is discouraged

      **Example:** A .ts file containing 6 seconds of H.264 1080p50 video, stored in S3. It is referenced by a Segment on the live recording Flow, and also by two Segments on different highlight edit Flows — three uses, one copy of the media.

  - title: Storage
    icon: fa-database
    summary: The underlying object storage layer where media Objects physically reside — abstracted by the TAMS API and supporting multiple backends.
    detail: |
      **Storage** is the underlying persistence layer where media Objects physically reside. TAMS abstracts all access to storage through the API, so clients never need direct storage credentials.

      **Key points:**
      - TAMS uses standard cloud object storage (e.g. S3) — the API is storage-agnostic and supports multiple storage backends
      - The API provides pre-signed URLs so clients upload and download media directly, with TAMS managing access control
      - Storage backends are identified by UUID and advertised via the `/service/storage_backends` endpoint — clients can specify which backend to use when requesting storage allocation
      - Multiple backends enable: tiered storage (hot/warm/cold), cost allocation, geographical distribution, and fine-grained access control
      - The store manages Object lifecycle: reference counting tracks which Objects are still in use, and unused Objects are cleaned up
      - "Orphaned" Objects (uploaded but never registered against a Segment) are tracked from the point of creation and can be cleaned up by the implementation
      - Retention management can be signalled via tags (`flow_retention_offset`, `segment_retention_offset`) to enable automated lifecycle policies
      - Object Instances allow the same Object to exist across multiple storage backends for redundancy or performance

      **Example:** A deployment with two storage backends: "hot" (S3 Standard, eu-west-1) for live content and recent edits, and "archive" (S3 Glacier, eu-west-2) for completed programmes. The TAMS API manages all access, and content can be moved between tiers without changing any Flow or Segment references.

  - title: Tags
    icon: fa-tag
    summary: Key-value metadata attached to Sources and Flows for content discovery, filtering, workflow automation, and access control.
    detail: |
      **Tags** are key-value pairs attached to Sources and Flows that enable content discovery, filtering, workflow automation, and lightweight access control.

      **Key points:**
      - Tags are applied at both the Source and Flow level — Source tags describe content editorially; Flow tags describe technical or workflow state
      - Values can be strings or arrays (as of API v8.0), providing flexibility for multi-value scenarios like language codes
      - Tags are searchable — you can query the store to find all Sources or Flows matching specific tag values
      - When a Source is auto-created from a Flow, the AWS implementation copies the Flow's tags to the Source (this is optional in the specification)
      - Tags can also be used to trial metadata fields before they are elevated to the core API specification
      - Known registered tags include: `flow_status` (e.g. `active`, `closed_complete`, `replication_in_progress`), `input_quality` (e.g. `intermediate`, `contribution`, `web`), `language_code` (ISO 639-3), `c2pa-provenance`, `auth_classes`, and retention tags
      - Tags on webhooks enable event-driven automation — downstream systems can watch for specific tag values to trigger workflows
      - For interoperability, tags used across multiple systems or vendors should be registered in App Note 0003 to prevent compatibility issues

      **Example:** A Source tagged with `language_code: eng` and `auth_classes: news-team,editors`. Its Flows tagged with `flow_status: active`, `input_quality: contribution`, and `segment_retention_offset: 604800:0` (auto-delete segments after 7 days). A QC system watches for `flow_status: active` and triggers automated quality checks.
---

## Key TAMS Concepts

The TAMS data model is built around a number of key concepts. Click any card below to learn more about how each element works and how they relate to each other.
