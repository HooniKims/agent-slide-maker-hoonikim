---
name: hyperframes-slide-work-image-left
description: Use when creating or editing a 16:9 HyperFrames slide where one main image should sit on the left and the explanation, bullets, or question block should stay on the right.
---

# Image Left Slide

Use this template when the image should be seen first and the explanation should follow on the right.

## Structure

```html
<section id="s-N" class="scene clip image-left"
  data-skill="image-left"
  data-start="..." data-duration="7" data-track-index="0">
  <div class="visual">
    <img src="assets/generated/example.png" alt="Short image description">
  </div>
  <div class="text-side">
    <div class="kicker">Section</div>
    <h1 class="headline">Main message</h1>
    <p class="subtext">Optional supporting sentence.</p>
    <ul class="bullet-list">
      <li>Point 1</li>
      <li>Point 2</li>
    </ul>
    <p class="note">Optional note.</p>
  </div>
</section>
```

## CSS Pattern

```css
.image-left{
  display:grid;
  grid-template-columns:1.22fr 0.78fr;
  gap:56px;
  align-items:center;
}
.image-left .visual{grid-column:1;grid-row:1;height:690px;overflow:hidden}
.image-left .text-side{grid-column:2;grid-row:1;position:relative;z-index:2;min-width:0}
.image-left .headline{font-size:68px;max-width:820px}
.image-left .bullet-list{margin-top:36px;gap:18px;max-width:820px}
.image-left .bullet-list li{font-size:32px;line-height:1.36}
.image-left .visual img{width:100%;height:100%;object-fit:contain;object-position:center center}
.image-left .note{margin-top:18px}
```

## Use For

- Demonstration slides where the visual object is the starting point.
- Before/after or screenshot explanation where the image needs more space.
- Slides where the right text should behave like a caption, interpretation, or prompt.

## Editing Guidance

- Put the main visual in `.visual`; avoid nesting extra cards around it.
- Keep the right text smaller than a full hero headline when it acts as explanation.
- If the image is cropped, adjust `object-position`, `transform`, or the `.visual` height before changing the deck structure.
