---
name: hyperframes-slide-work-image-right
description: Use when creating or editing a 16:9 HyperFrames slide where text, bullets, or a question block should stay on the left and one main image should sit on the right.
---

# Image Right Slide

Use this template when the audience should read the idea first and then inspect one supporting image on the right.

## Structure

```html
<section id="s-N" class="scene clip image-right"
  data-skill="image-right"
  data-start="..." data-duration="7" data-track-index="0">
  <div class="text-side">
    <div class="kicker">Section</div>
    <h1 class="headline">Main message</h1>
    <p class="subtext">Optional supporting sentence.</p>
    <ul class="bullet-list">
      <li>Point 1</li>
      <li>Point 2</li>
    </ul>
    <p class="note">Optional activity or QR instruction.</p>
  </div>
  <div class="visual">
    <img src="assets/generated/example.png" alt="Short image description">
  </div>
</section>
```

## CSS Pattern

```css
.image-right{
  display:grid;
  grid-template-columns:0.78fr 1.22fr;
  gap:56px;
  align-items:center;
}
.image-right .text-side{grid-column:1;grid-row:1;position:relative;z-index:2;min-width:0}
.image-right .headline{font-size:68px;max-width:820px}
.image-right .bullet-list{margin-top:36px;gap:18px;max-width:820px}
.image-right .bullet-list li{font-size:32px;line-height:1.36}
.image-right .visual{grid-column:2;grid-row:1;height:690px;overflow:hidden}
.image-right .visual img{width:100%;height:100%;object-fit:contain;object-position:center center}
.image-right .note{margin-top:18px}
```

## Use For

- Concept explanation with one metaphor image.
- Activity prompt with a QR code or short note under the text.
- Slides where the text is the reading path and the image is the memory hook.

## Editing Guidance

- Keep the left text concise enough that it does not collide with the image.
- If the image needs more emphasis, increase the right grid column or set an inline `visual_style`.
- If the user asks to move or crop the image, change the `.visual img` transform or `object-position` rather than rewriting the text.
