---
layout: page
permalink: /brand/
kicker: Resources
title: Brand Guidelines
subtitle: The TAMS visual identity — open, and free for everyone to use.
hero_image: /images/resources_background.png
---

The TAMS visual identity is built from the specification itself. The mark is **four media segments across two timeline tracks**, staggered so the negative space reads as a **T**. There are no curves, no gradients and no illustration — just simple shapes on a grid, which means it stays legible stamped at 16 pixels, printed in a single ink, or stitched into fabric.

## The mark

The mark is drawn on a fixed **24 × 12 unit grid**: two 5-unit tracks separated by a 2-unit gutter. The top track carries Playhead Amber; the bottom track carries the foreground colour. It sits beside the Geist Bold wordmark (horizontal) or above it (stacked), and works on dark or light backgrounds.

<svg width="0" height="0" style="position:absolute" aria-hidden="true"><symbol id="tams-mark" viewBox="0 0 24 12"><rect x="0" y="0" width="14" height="5" fill="var(--acc,currentColor)"></rect><rect x="16" y="0" width="8" height="5" fill="var(--acc,currentColor)"></rect><rect x="0" y="7" width="6" height="5" fill="currentColor"></rect><rect x="8" y="7" width="16" height="5" fill="currentColor"></rect></symbol></svg>

<div class="brand-lockups">
  <figure>
    <div class="brand-lockup dark"><span class="lk"><svg class="mk" width="48" height="24" viewBox="0 0 24 12" style="--acc:#E5A144"><use href="#tams-mark"></use></svg><span class="wm">TAMS</span></span></div>
    <figcaption>Horizontal · on Control Navy</figcaption>
  </figure>
  <figure>
    <div class="brand-lockup light"><span class="lk"><svg class="mk" width="48" height="24" viewBox="0 0 24 12" style="--acc:#E5A144"><use href="#tams-mark"></use></svg><span class="wm">TAMS</span></span></div>
    <figcaption>Horizontal · on Paper</figcaption>
  </figure>
  <figure>
    <div class="brand-lockup dark"><span class="lk stacked"><svg class="mk" width="56" height="28" viewBox="0 0 24 12" style="--acc:#E5A144"><use href="#tams-mark"></use></svg><span class="wm">TAMS</span></span></div>
    <figcaption>Stacked · on Control Navy</figcaption>
  </figure>
  <figure>
    <div class="brand-lockup light"><span class="lk stacked"><svg class="mk" width="56" height="28" viewBox="0 0 24 12" style="--acc:#E5A144"><use href="#tams-mark"></use></svg><span class="wm">TAMS</span></span></div>
    <figcaption>Stacked · on Paper</figcaption>
  </figure>
</div>

- **Clearspace** — keep clear space of at least one track height on all sides.
- **Minimum sizes** — avatar at 48 / 32 / 24 px, favicon at 16 px. Below 24 px, use the mark inside its rounded navy **tile**, not the bare mark.
- **Single colour** — where duotone isn't possible, the mark works in any single colour with all four segments equal.

## Colour

A broadcast-gallery navy with a single amber accent — the playhead. **Amber is reserved for emphasis** (the top track, cursors, links, highlights); never use it for body text or large fills.

<div class="brand-palette">
  <div class="brand-swatch"><div class="chip" style="background:#141A28"></div><div class="lbl"><b>Control Navy</b><code>#141A28</code><span class="role">Primary background · ink on light.</span></div></div>
  <div class="brand-swatch"><div class="chip" style="background:#FFFFFF"></div><div class="lbl"><b>Signal White</b><code>#FFFFFF</code><span class="role">Text on dark · UI surfaces.</span></div></div>
  <div class="brand-swatch"><div class="chip" style="background:#F5F4F0"></div><div class="lbl"><b>Paper</b><code>#F5F4F0</code><span class="role">Light backgrounds · documents.</span></div></div>
  <div class="brand-swatch"><div class="chip" style="background:#E5A144"></div><div class="lbl"><b>Playhead Amber</b><code>#E5A144</code><span class="role">Accent only · top track · links.</span></div></div>
</div>

## Typography

**Geist** for the wordmark, headlines, UI and body copy. **IBM Plex Mono** for anything machine-adjacent — endpoints, IDs, labels and timeranges. Both typefaces are under the SIL Open Font License.

<div class="type-showcase">
  <div class="type-card">
    <div class="tk">Geist</div>
    <div class="big" style="font-weight:700;font-size:40px">Geist Bold</div>
    <div class="specimen" style="font-size:18px">Geist Regular for body copy.<br>Aa Bb Cc Dd Ee &mdash; 0 1 2 3 4 5 6 7 8 9</div>
    <div class="role">wordmark · headlines · UI · body</div>
  </div>
  <div class="type-card mono">
    <div class="tk">IBM Plex Mono</div>
    <div class="big" style="font-weight:500;font-size:28px">IBM Plex Mono</div>
    <div class="specimen" style="font-size:13.5px">GET /flows/{flowId}/segments<br>?timerange=[0:0_10:0)</div>
    <div class="role">descriptor · labels · code · timeranges</div>
  </div>
</div>

## Download

Everything is open — no request form, no licence fee. The logo kit ships as SVG (outlined type, no fonts required) and transparent PNG. If you need a format that isn't in the kit, open an issue on the [TAMS repository](https://github.com/bbc/tams) and it'll be added for everyone.

- [Download the TAMS Brand Kit (ZIP)]({{ '/resources/brand-kit/TAMS_Brand_Kit_v1.2.zip' | relative_url }})
- [View the Brand Identity Document (PDF)]({{ '/resources/brand-kit/TAMS_Brand_Identity_Doc_v1.2.pdf' | relative_url }})
