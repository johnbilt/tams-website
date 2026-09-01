---
layout: guide
permalink: /guide/edit-by-reference/
kicker: Guide
title: Guide to Working With TAMS
subtitle: Edit By Reference
hero_image: /images/resources_background.png
---

In a traditional edit workflow all the frames of the new edit need to be rendered into a new file which is then written out to storage.  For many simple edits the actual content can be largely unchanged, however the essence needs to be duplicated in order to have a file which can be played back directly.

The TAMS store holds the media in very small Segments - typically a few seconds in duration. This opens up interesting possibilities when editing content where the frames are unchanged, allowing us to reference the existing media instead of duplicating it.  This not only means that less storage space is required by de-duplicating the content, but time is saved at the export stage from the edit system, as the time taken to render a new asset is no longer required, it is replaced with an API call.

To re-use an existing Segment within a new Flow then it is a case of registering it as a Segment for the new Flow referencing the same Object ID as the Object was originally created with.  The store will recognise the same ID and create the link in the background.

When declaring the reused segment, the timerange should be updated to the location where the Segment exists on the new Flow timeline.  If the timing has changed the the new segment will also need the ts_offset field to be set to ensure that the player understands there is difference between the timing data in the media segment and the new timeline.

For edits where some content on the timeline is new or has changed then this will need to be rendered out and uploaded to the store as new Segments.  It is possible to mix both existing and new Segments on a new Flow timeline.  This means that a simple edit with a dissolve between two unchanged clips would only need the frames for the dissolve to the rendered and uploaded as new Segments.  All the other content would be references to existing Segments.

App Note 15 in the TAMS API repo has more information about rendering edited content back to a TAMS store.  It also covers how to reference content in a TAMS store within the OpenTimelineIO format to describe content edits:  
[https://github.com/bbc/tams/blob/aaefef3126606a02b73e4c9e24761364a5d5586a/docs/appnotes/0015-using-tams-in-opentimelineio.md#rendering-back-to-tams](https://github.com/bbc/tams/blob/aaefef3126606a02b73e4c9e24761364a5d5586a/docs/appnotes/0015-using-tams-in-opentimelineio.md#rendering-back-to-tams){:target="_blank"}

### Frame Accurate Working

In a typical TAMS workflow then the Segments are usually between around 1 and 10 seconds in duration.  This means that working at a Segment level for editing will not result in a frame accurate level of editing.  While this may be acceptable for some use cases, this will not be considered acceptable for most workflows.

There are two options available to carry out frame accurate edits within a TAMS environment:

1. Within the Segment metadata it is possible to define only part of the Segment should be used within the new flow timeline.  This approach requires the reading system to understand all the details of the Segment supplied by the API and be able to play just part of a Segment

2. For workflows which need to work at a Segment level (for example converting to an HLS stream) then the only option is to render the part of the boundary Segment.  By creating the new smaller subsegment and uploading it to the store then the player will receive a constant stream of whole Segments to play back.  Only the boundary Segments need to be created, all other Segments can remain as pointers.

Clearly the first option should be the preferred route as this is both efficient in terms of storage, complete and time, however it is recognised that this will not always be possible hence the second approach.

### Working With Multiple Flows

When creating content via an edit by reference workflow then it is important that all the original content being used within the edit have matching Flows.  This is due to a Source level edit needing to be applied to each of the Flows for a Source.  If one of the pieces of original content does not have all the Flows present then the resulting edit will have holes in the timeline.

The next challenge is matching Flows from the different pieces of original content.  The current approach would be to do the following:

1. For the first section of content required then copy the technical details of all the Flows from the first source to the create a new set of Flows and Sources to represent the edit

2. While creating the new Flows create a hash of core technical parameters (eg resolution, bitrate, codec, frame rate) and store

3. Copy the Segments from the Flows in the first piece of content into the newly created destination Flows

4. For the second section of required content then read the Flows available and generate the same technical parameter hash generated earlier.  Using this it would then be able to match the original Flows to the target Flows

5. Copy the Segments from the original Flows to the matched target Flows

6. Repeat steps 4 and 5 for each section of required source content.

While creating the new Segments ensure that the new timerange is specified for where the Segment should exist on the new Flow timeline.  Additionally the `ts_offset` should be declared to indicate the difference between the timing data in the media files and the new Flow timeline position.
