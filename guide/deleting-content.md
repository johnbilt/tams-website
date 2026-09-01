---
layout: guide
permalink: /guide/deleting-content/
kicker: Guide
title: Guide to Working With TAMS
subtitle: Deleting Content
hero_image: /images/resources_background.png
---

Within TAMS all content deletions happen at the Flow level.  There are three ways that content can be deleted:

1. Delete the whole of a Flow and all Segments beneath it
2. By deleting an individual Segment
3. Deleting part of a Flow by specifying the timerange to be deleted.

In all scenarios the TAMS store will process the delete in such a manner that the Segments linked to the Flow will appear to delete immediately and no longer be available for use.  Depending on the implementation of the store then there may be a delay between the initial delete request processing and the actual removal of the Objects from the object storage.  In the AWS Open Source TAMS API this is set to 1 hour by default.

For Objects which are referenced in multiple Flows, the store is responsible for managing the housekeeping of them.  When a delete request is made the store will check if the Object is referenced in any other Flows.  If there are no other references then the store will queue the Object for deletion.  If the Object is used in other Flows then the pointer from the Flow will be removed but the Object will remain in place until all references are removed.

Where a delete request will take longer than the time available to respond to a synchronous API call, the store can chose to create a delete task for asynchronous processing.  There is a dedicated API endpoint to track progress of these requests.
