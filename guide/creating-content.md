---
layout: guide
permalink: /guide/creating-content/
kicker: Guide
title: Guide to Working With TAMS
subtitle: Creating Content
hero_image: /images/resources_background.png
---

The TAMS data model is built up step by step. Flows are the primary element you create — Sources and their relationships are managed automatically by the store. Use the controls below to walk through the creation sequence.

<style>
  .dc-container {
    display: flex;
    gap: 1.5rem;
    align-items: stretch;
    min-height: 480px;
  }
  @media screen and (max-width: 768px) {
    .dc-container {
      flex-direction: column-reverse;
    }
  }
  .dc-diagram {
    flex: 2;
    position: relative;
  }
  .dc-info {
    flex: 1;
    border-right: 4px solid #141A28;
    padding: 1.25rem;
    background: #f8fafd;
    border-radius: 4px;
    overflow-y: auto;
    max-height: 650px;
    display: flex;
    flex-direction: column;
  }
  .dc-info h3 {
    margin-top: 0;
    color: #141A28;
  }
  .dc-info .step-description {
    flex: 1;
  }
  .dc-controls {
    display: flex;
    gap: 0.5rem;
    margin-top: 1rem;
    padding-top: 0.75rem;
    border-top: 1px solid #e0e0e0;
    align-items: center;
  }
  .dc-controls button {
    padding: 0.4rem 1rem;
    border: 2px solid #141A28;
    background: #fff;
    color: #141A28;
    border-radius: 4px;
    cursor: pointer;
    font-weight: 600;
    font-size: 0.85rem;
    transition: all 0.2s;
  }
  .dc-controls button:hover:not(:disabled) {
    background: #141A28;
    color: #fff;
  }
  .dc-controls button:disabled {
    opacity: 0.4;
    cursor: not-allowed;
  }
  .dc-controls .step-indicator {
    margin-left: auto;
    font-size: 0.8rem;
    color: #666;
  }

  .dc-diagram svg {
    width: 100%;
    height: 100%;
    min-height: 480px;
  }
  .dc-node {
    opacity: 0;
    transition: opacity 0.5s ease;
  }
  .dc-node.visible {
    opacity: 1;
  }
  .dc-node rect {
    stroke-width: 2;
    rx: 8;
    ry: 8;
  }
  .dc-node.highlight rect {
    stroke-width: 3.5;
    filter: drop-shadow(0 2px 8px rgba(0,0,0,0.25));
  }
  .dc-node text {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    fill: #333;
    text-anchor: middle;
    pointer-events: none;
  }
  .dc-node text.node-label {
    font-size: 11px;
    font-weight: 600;
  }
  .dc-node text.node-sublabel {
    font-size: 9.5px;
    fill: #555;
  }
  .dc-node text.node-icon {
    font-family: "Font Awesome 6 Free";
    font-weight: 900;
    font-size: 14px;
    fill: #fff;
  }
  .dc-link {
    fill: none;
    stroke-width: 1.5;
    opacity: 0;
    transition: opacity 0.5s ease;
  }
  .dc-link.visible {
    opacity: 0.5;
  }
  .dc-link.belongs {
    stroke: #555;
  }
  .dc-link.collection {
    stroke: #141A28;
    stroke-dasharray: 5,3;
  }
  .dc-link.visible.collection {
    opacity: 0.6;
  }
  .dc-action-label {
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    font-size: 9px;
    fill: #27ae60;
    font-weight: 600;
    text-anchor: middle;
    opacity: 0;
    transition: opacity 0.5s ease;
  }
  .dc-action-label.visible {
    opacity: 1;
  }
</style>

<div class="dc-container">
  <div class="dc-info" id="dc-info-panel">
    <div class="step-description" id="dc-step-text">
      <h3>Step 1: Create Video Flow</h3>
      <p>Create a <strong>Video Flow</strong> specifying the technical parameters (codec, resolution, frame rate) and a Source ID to link to.</p>
      <p><strong>What you do:</strong> POST to create a video Flow with a source_id</p>
    </div>
    <div class="dc-controls">
      <button id="dc-prev" disabled>Previous</button>
      <button id="dc-next">Next</button>
      <button id="dc-reset">Reset</button>
      <span class="step-indicator" id="dc-step-indicator">Step 1 / 7</span>
    </div>
  </div>

  <div class="dc-diagram">
    <svg viewBox="0 0 580 480" preserveAspectRatio="xMidYMid meet">
      <defs>
        <marker id="c-arrow" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
          <path d="M0,0 L8,3 L0,6 Z" fill="#555" opacity="0.5"/>
        </marker>
        <marker id="c-arrow-blue" markerWidth="8" markerHeight="6" refX="8" refY="3" orient="auto">
          <path d="M0,0 L8,3 L0,6 Z" fill="#141A28" opacity="0.6"/>
        </marker>
      </defs>

      <!-- === LINKS === -->

      <!-- Video Flow → Video Source (belongs) -->
      <line class="dc-link belongs" data-step="2" x1="150" y1="270" x2="150" y2="150" marker-end="url(#c-arrow)"/>

      <!-- Audio Flow → Audio Source (belongs) -->
      <line class="dc-link belongs" data-step="4" x1="420" y1="270" x2="420" y2="150" marker-end="url(#c-arrow)"/>

      <!-- Multi Flow → Multi Source (belongs) -->
      <line class="dc-link belongs" data-step="6" x1="290" y1="185" x2="290" y2="65" marker-end="url(#c-arrow)"/>

      <!-- Multi Flow → Video Flow (collection) -->
      <path class="dc-link collection" data-step="5" d="M240,235 C240,255 150,255 150,270" marker-end="url(#c-arrow-blue)"/>
      <!-- Multi Flow → Audio Flow (collection) -->
      <path class="dc-link collection" data-step="5" d="M340,235 C340,255 420,255 420,270" marker-end="url(#c-arrow-blue)"/>

      <!-- Multi Source → Video Source (collection) -->
      <path class="dc-link collection" data-step="6" d="M260,65 C250,82 150,82 150,100" marker-end="url(#c-arrow-blue)"/>
      <!-- Multi Source → Audio Source (collection) -->
      <path class="dc-link collection" data-step="6" d="M320,65 C330,82 420,82 420,100" marker-end="url(#c-arrow-blue)"/>

      <!-- Segment lines to flows -->
      <line class="dc-link belongs" data-step="7" x1="150" y1="355" x2="150" y2="320" marker-end="url(#c-arrow)"/>
      <line class="dc-link belongs" data-step="7" x1="420" y1="355" x2="420" y2="320" marker-end="url(#c-arrow)"/>

      <!-- === ROW 1: Multi-Essence Source === -->
      <g class="dc-node" data-step="6" data-node="multi-source">
        <rect x="205" y="15" width="170" height="50" fill="#e8f4f8" stroke="#0077b6"/>
        <circle cx="240" cy="40" r="12" fill="#0077b6"/>
        <text class="node-icon" x="240" y="44">&#xf0e8;</text>
        <text class="node-label" x="315" y="37">Programme</text>
        <text class="node-sublabel" x="315" y="50">Multi-Essence Source</text>
      </g>

      <!-- === ROW 2: Mono Sources === -->
      <g class="dc-node" data-step="2" data-node="video-source">
        <rect x="75" y="100" width="150" height="50" fill="#e8f4f8" stroke="#0077b6"/>
        <circle cx="110" cy="125" r="12" fill="#0077b6"/>
        <text class="node-icon" x="110" y="129">&#xf03d;</text>
        <text class="node-label" x="175" y="122">Video</text>
        <text class="node-sublabel" x="175" y="135">Source</text>
      </g>

      <g class="dc-node" data-step="4" data-node="audio-source">
        <rect x="345" y="100" width="150" height="50" fill="#e8f4f8" stroke="#0077b6"/>
        <circle cx="380" cy="125" r="12" fill="#0077b6"/>
        <text class="node-icon" x="380" y="129">&#xf130;</text>
        <text class="node-label" x="445" y="122">Audio</text>
        <text class="node-sublabel" x="445" y="135">Source</text>
      </g>

      <!-- === ROW 3: Multi-Essence Flow === -->
      <g class="dc-node" data-step="5" data-node="multi-flow">
        <rect x="205" y="185" width="170" height="50" fill="#fef3e8" stroke="#e67e22"/>
        <circle cx="240" cy="210" r="12" fill="#e67e22"/>
        <text class="node-icon" x="240" y="214">&#xf0e8;</text>
        <text class="node-label" x="315" y="207">Programme</text>
        <text class="node-sublabel" x="315" y="220">Multi-Essence Flow</text>
      </g>

      <!-- === ROW 4: Mono Flows === -->
      <g class="dc-node" data-step="1" data-node="video-flow">
        <rect x="75" y="270" width="150" height="50" fill="#fef3e8" stroke="#e67e22"/>
        <circle cx="110" cy="295" r="12" fill="#e67e22"/>
        <text class="node-icon" x="110" y="299">&#xf03d;</text>
        <text class="node-label" x="175" y="292">1080p50 H.264</text>
        <text class="node-sublabel" x="175" y="305">Video Flow</text>
      </g>

      <g class="dc-node" data-step="3" data-node="audio-flow">
        <rect x="345" y="270" width="150" height="50" fill="#fef3e8" stroke="#e67e22"/>
        <circle cx="380" cy="295" r="12" fill="#e67e22"/>
        <text class="node-icon" x="380" y="299">&#xf130;</text>
        <text class="node-label" x="445" y="292">48kHz PCM</text>
        <text class="node-sublabel" x="445" y="305">Audio Flow</text>
      </g>

      <!-- === ROW 5: Segments === -->
      <g class="dc-node" data-step="7" data-node="video-segments">
        <rect x="75" y="355" width="150" height="40" fill="#f0f0f0" stroke="#888"/>
        <text class="node-label" x="150" y="379">Video Segments</text>
      </g>

      <g class="dc-node" data-step="7" data-node="audio-segments">
        <rect x="345" y="355" width="150" height="40" fill="#f0f0f0" stroke="#888"/>
        <text class="node-label" x="420" y="379">Audio Segments</text>
      </g>

      <!-- === ACTION LABELS === -->
      <text class="dc-action-label" data-step="1" x="150" y="263">CREATE</text>
      <text class="dc-action-label" data-step="2" x="150" y="93" style="fill: #0077b6;">AUTO-CREATED</text>
      <text class="dc-action-label" data-step="3" x="420" y="263">CREATE</text>
      <text class="dc-action-label" data-step="4" x="420" y="93" style="fill: #0077b6;">AUTO-CREATED</text>
      <text class="dc-action-label" data-step="5" x="290" y="178">CREATE + COLLECT</text>
      <text class="dc-action-label" data-step="6" x="290" y="8" style="fill: #0077b6;">AUTO-CREATED + COLLECTED</text>
      <text class="dc-action-label" data-step="7" x="290" y="410">UPLOAD + REGISTER</text>

      <!-- === LEGEND === -->
      <g transform="translate(20, 430)">
        <text font-size="10" font-weight="600" fill="#333" font-family="sans-serif">Legend:</text>

        <line x1="60" y1="0" x2="95" y2="0" stroke="#555" stroke-width="1.5" opacity="0.5"/>
        <polygon points="95,-3 101,0 95,3" fill="#555" opacity="0.5"/>
        <text x="108" y="4" font-size="10" fill="#666" font-family="sans-serif">Belongs to</text>

        <line x1="200" y1="0" x2="235" y2="0" stroke="#141A28" stroke-width="1.5" stroke-dasharray="5,3" opacity="0.6"/>
        <polygon points="235,-3 241,0 235,3" fill="#141A28" opacity="0.6"/>
        <text x="248" y="4" font-size="10" fill="#666" font-family="sans-serif">Collection</text>

        <rect x="350" y="-7" width="14" height="14" rx="3" fill="#e8f4f8" stroke="#0077b6" stroke-width="1.5"/>
        <text x="370" y="4" font-size="10" fill="#666" font-family="sans-serif">Source</text>

        <rect x="430" y="-7" width="14" height="14" rx="3" fill="#fef3e8" stroke="#e67e22" stroke-width="1.5"/>
        <text x="450" y="4" font-size="10" fill="#666" font-family="sans-serif">Flow</text>
      </g>
    </svg>
  </div>
</div>

<script>
(function() {
  var currentStep = 1;
  var totalSteps = 7;

  var stepDescriptions = {
    1: {
      title: 'Step 1: Create Video Flow',
      content: '<p>Create a <strong>Video Flow</strong> specifying the technical parameters (codec, resolution, frame rate) and a Source ID to link to.</p><p><strong>What you do:</strong> POST to create a video Flow with a source_id</p>'
    },
    2: {
      title: 'Step 2: Video Source Auto-Created',
      content: '<p>The Source ID referenced by the Video Flow does not exist in the store, so the store <strong>automatically creates the Video Source</strong>.</p><p>The Source inherits the label and description from the Flow.</p><p><strong>What the store does:</strong> Creates the Video Source and links the Flow to it</p>'
    },
    3: {
      title: 'Step 3: Create Audio Flow',
      content: '<p>Create an <strong>Audio Flow</strong> with its technical parameters (sample rate, bit depth, codec) and a new Source ID.</p><p><strong>What you do:</strong> POST to create an audio Flow with a new source_id</p>'
    },
    4: {
      title: 'Step 4: Audio Source Auto-Created',
      content: '<p>The Source ID referenced by the Audio Flow does not exist, so the store <strong>automatically creates the Audio Source</strong>.</p><p><strong>What the store does:</strong> Creates the Audio Source and links the Flow to it</p>'
    },
    5: {
      title: 'Step 5: Create Multi-Essence Flow with Collection',
      content: '<p>Create a <strong>Multi-Essence Flow</strong> referencing a new Source ID and specifying the Video and Audio Flows as part of its collection.</p><p>This Flow has no media stored against it — it represents the combined programme.</p><p><strong>What you do:</strong> POST to create a multi-essence Flow, including the video and audio Flow IDs in the collection</p>'
    },
    6: {
      title: 'Step 6: Multi-Essence Source Auto-Created',
      content: '<p>The store <strong>automatically creates the Multi-Essence Source</strong> and resolves the collection relationships — linking the Video Source and Audio Source into the Multi-Essence Source\'s collection.</p><p><strong>What the store does:</strong> Creates the Multi-Essence Source, creates collection links between all Sources based on the Flow collections</p>'
    },
    7: {
      title: 'Step 7: Upload and Register Segments',
      content: '<p><strong>Upload media segments</strong> to object storage using pre-signed URLs from the API, then register each segment against the appropriate Flow with its timerange.</p><p>Segments are registered against the mono-essence Flows only (Video Flow and Audio Flow). The Multi-Essence Flow has no segments.</p><p><strong>What you do:</strong> Request pre-signed URLs, upload media, then POST to register segments with their timeranges</p>'
    }
  };

  var prevBtn = document.getElementById('dc-prev');
  var nextBtn = document.getElementById('dc-next');
  var resetBtn = document.getElementById('dc-reset');
  var stepText = document.getElementById('dc-step-text');
  var stepIndicator = document.getElementById('dc-step-indicator');

  function updateDiagram() {
    var nodes = document.querySelectorAll('.dc-node');
    var links = document.querySelectorAll('.dc-link');
    var labels = document.querySelectorAll('.dc-action-label');

    nodes.forEach(function(node) {
      var step = parseInt(node.getAttribute('data-step'));
      if (step <= currentStep) {
        node.classList.add('visible');
        if (step === currentStep) {
          node.classList.add('highlight');
        } else {
          node.classList.remove('highlight');
        }
      } else {
        node.classList.remove('visible');
        node.classList.remove('highlight');
      }
    });

    links.forEach(function(link) {
      var step = parseInt(link.getAttribute('data-step'));
      if (step <= currentStep) {
        link.classList.add('visible');
      } else {
        link.classList.remove('visible');
      }
    });

    labels.forEach(function(label) {
      var step = parseInt(label.getAttribute('data-step'));
      if (step === currentStep) {
        label.classList.add('visible');
      } else {
        label.classList.remove('visible');
      }
    });

    var desc = stepDescriptions[currentStep];
    stepText.innerHTML = '<h3>' + desc.title + '</h3>' + desc.content;

    prevBtn.disabled = (currentStep === 1);
    nextBtn.disabled = (currentStep === totalSteps);
    stepIndicator.textContent = 'Step ' + currentStep + ' / ' + totalSteps;
  }

  nextBtn.addEventListener('click', function() {
    if (currentStep < totalSteps) {
      currentStep++;
      updateDiagram();
    }
  });

  prevBtn.addEventListener('click', function() {
    if (currentStep > 1) {
      currentStep--;
      updateDiagram();
    }
  });

  resetBtn.addEventListener('click', function() {
    currentStep = 1;
    updateDiagram();
  });

  updateDiagram();
})();
</script>

---

## Detailed Creation Process

When creating content within a TAMS store the sequence of creating the different elements matters. The most important element to create are the Flows.

When creating a Flow, it includes a reference to the Source to which it belongs.  If the Source exists within the store then the two will be linked, however if the Source does not exist then the store will automatically create it.  

When a Source is created the label and description fields from the Flow will initially be replicated to the Source.  It is up to the store implementation whether the tags from the Flow will be replicated to the Source - the AWS open source implementation does but it is optional in the specification.  Once the Source is created it is then possible to call the TAMS API and update the label or description as well as add tags required.

If creating a multi-essence Flow, any mono-essence Flows which are to be collected by it must exist in the store prior to creating the Flow collection. The creation of a multi-essence Flow will cause a multi-essence Source to be created by the store. This new Source will automatically collect any other Sources associated to the Flows collected by the multi-essence Flow.

If new Flows are to be added to an existing multi Flow then they must be created and then added to the collection.  The store in turn will ripple the collections up from the Flow to Source level.

Within the store it is not possible to create Sources directly, these are created and deleted along with their associated Flows.

### Creating New Mono Essence Sources and Flows

To store mono-essence media within TAMS, the first step is to create the separate mono-essence Flows.  These hold the technical characteristics of the segments registered to them.  It is possible to have multiple Flows representing the same content.  For example the video may have multiple different resolutions, bit rates, codecs or frame rates.  Each variant would be stored as a separate Flow, but would be registered with the same Source ID.

On creation of the mono-essence Flows the relevant Source(s) will be automatically created in the TAMS store.  At this point the different media types will still be separate elements.

![Diagram showing the sequence of creating the different elements within the TAMS data model](/images/creation_sequence.png)

To represent the combination of audio and video into a single version, a multi-essence Flow should be created.  This flow has no essence parameters as there is no media stored against it.  The multi-flow definition includes a collection element and this should include the IDs and roles of all Flows to be collected together.

Flow collections can only be created or removed against the multi-flow.  The store will manage the collections automatically, such that querying against a mono-essence Flow will list all the Flows it is collected by, but these cannot be modified against the mono-essence Flow.

On creation of the multi-essence Flow the corresponding multi-essence Source will be created.  Where the Flow collects other Flows then the store will automatically resolve the links to the relevant sources and create the corresponding Source collection links.  The creating system does not need to create the Source collections directly

App Note 007 in the TAMS API repo describes how Source metadata is populated within a store:
[https://github.com/bbc/tams/blob/aaefef3126606a02b73e4c9e24761364a5d5586a/docs/appnotes/0007-populating-source-metadata.md](https://github.com/bbc/tams/blob/aaefef3126606a02b73e4c9e24761364a5d5586a/docs/appnotes/0007-populating-source-metadata.md){:target="_blank"}

### Registering Segments

To simplify the need for both API and storage credentials, the TAMS API will supply pre-signed URLs for media Objects to be uploaded to.  This is done by calling the storage endpoint for a given Flow and requesting the required number of pre-signed URLs.

The creating system then uploads the media Object directly to the object storage using the pre-signed URL.  No other credentials are required for this process.

After upload, the creating system then needs to call the TAMS API and register the Object against the given Flow.  As part of the registration, the creating system will declare the timerange where the Segment sits within the Flow timeline.  For the initial Segment registration the timing metadata within the media file is expected to match the timerange for the Segment.

![Diagram showing the sequence of registering segments with the store](/images/segment_sequence.png)

For [Edit by Reference]({{ '/guide/edit-by-reference/' | relative_url }}) workflows it is possible to re-use a Segment.  This is done by registering a Segment on the new Flow timeline with the same Object ID as the original Object.  The store will recognise the Object re-use automatically.  At the point of registration it is also possible to specify only part of a Segment to be used and offsets from the internal file timing to that of the Flow timeline.
