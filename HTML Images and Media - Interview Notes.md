# HTML Images and Media — Interview Preparation

## 1. Image element: `<img>`

The `<img>` element embeds an image in a document:

```html
<img src="retina-fundus.jpg" alt="Fundus photograph showing the retinal surface">
```

- `<img>` is a **void element**: it has no closing tag and cannot contain child elements.
- Provide a valid `src` and an appropriate `alt` text.
- Use an image for content that belongs in the document. For purely decorative imagery, consider CSS backgrounds or an empty alternative such as `alt=""`.
- If an image cannot load, its alternative text provides a text equivalent when appropriate.

## 2. Image source: `src`

The `src` attribute specifies the image resource:

```html
<img src="images/fundus-study.png" alt="A fundus image used for a preprocessing example">
```

The source can be a relative path or a full URL. Check that the path is correct and that the browser can access the resource.

For modern responsive sources, use `<picture>` or `srcset` when different formats or files are appropriate; see the responsive images section.

## 3. Alternative text: `alt`

The `alt` attribute provides a text alternative for an image. Screen readers can announce it, and browsers may display it if the image is unavailable.

### Informative image

Describe the relevant information conveyed by the image:

```html
<img src="vessel-map.png" alt="Highlighted vessels branching from the center of the retinal image">
```

### Decorative image

Use an empty alternative when the image adds no information beyond nearby content:

```html
<img src="decorative-divider.png" alt="">
```

An empty `alt` tells assistive technology to ignore the image. Do not omit the attribute for an image that needs an alternative: missing `alt` and `alt=""` do not mean the same thing.

### Image as a link

If the image is the only content inside a link, its alternative text should describe the link destination or action:

```html
<a href="/gallery">
  <img src="gallery-preview.jpg" alt="Open the retinal image gallery">
</a>
```

**Interview answer:** Good alternative text communicates the image's purpose in context, not every visible detail. Avoid redundant phrases such as “image of” unless knowing that it is an image matters.

## 4. Image dimensions

The `width` and `height` attributes declare an image's intrinsic dimensions in CSS pixels:

```html
<img
  src="retina-fundus.jpg"
  alt="Fundus photograph"
  width="1200"
  height="800">
```

- Providing the correct intrinsic dimensions lets browsers reserve the image's aspect ratio before it loads, which helps reduce layout shifts.
- The displayed dimensions can still be controlled responsively with CSS.
- Do not set misleading dimensions that distort the image.

```css
img {
  max-width: 100%;
  height: auto;
}
```

Use `object-fit` and a deliberate container size when the design requires a crop:

```css
.thumbnail {
  width: 12rem;
  aspect-ratio: 4 / 3;
  object-fit: cover;
}
```

## 5. Responsive images

Responsive images help a browser choose an appropriate image for the device, viewport, or layout.

### `srcset` and `sizes`

Use `srcset` with width descriptors when the same image is available in multiple resolutions:

```html
<img
  src="fundus-800.jpg"
  srcset="fundus-400.jpg 400w, fundus-800.jpg 800w, fundus-1400.jpg 1400w"
  sizes="(max-width: 600px) 100vw, 700px"
  width="1400"
  height="930"
  alt="Fundus photograph used in an image-processing demonstration">
```

- Each `400w`, `800w`, or `1400w` value describes the corresponding file's intrinsic width.
- `sizes` tells the browser how wide the image is expected to appear at different layout conditions.
- The browser uses the available candidates, layout, and display conditions to choose an appropriate resource.

### `<picture>` for art direction or formats

Use `<picture>` when you need to choose among different crops or formats:

```html
<picture>
  <source media="(max-width: 600px)" srcset="fundus-crop-mobile.jpg">
  <source type="image/webp" srcset="fundus-study.webp">
  <img src="fundus-study.jpg" alt="A retinal image shown for preprocessing study">
</picture>
```

- The nested `<img>` is required and provides the fallback image and its alternative text.
- The browser selects a matching `<source>` when possible.
- Use `<picture>` for art direction or format selection; use `srcset` for resolution choices.

### Lazy loading

For images outside the initial viewport, `loading="lazy"` can defer loading until they are closer to view:

```html
<img src="results-panel.jpg" alt="Image preprocessing results panel" loading="lazy">
```

Avoid lazy-loading the main above-the-fold image when it is important to the initial page display. Browser loading priority can be tuned with `fetchpriority` when there is a good reason, but it should not be applied indiscriminately.

## 6. Figures and captions: `<figure>` and `<figcaption>`

`<figure>` groups self-contained content, such as an image, diagram, code example, or chart, with an optional caption in `<figcaption>`:

```html
<figure>
  <img
    src="preprocessing-stages.png"
    alt="Three panels show the original image, green channel, and contrast-enhanced preview">
  <figcaption>Example preprocessing stages for visual inspection.</figcaption>
</figure>
```

- The figure can be moved or referenced as a unit without disrupting the document's main flow.
- `<figcaption>` provides a caption or legend for the figure.
- A caption and `alt` text serve different purposes: the caption is visible to readers; `alt` supplies a text alternative for the image.
- Do not repeat the same text in both unless both serve a useful purpose.

## 7. Audio: `<audio>`

The `<audio>` element embeds playable audio:

```html
<audio controls preload="metadata">
  <source src="project-introduction.mp3" type="audio/mpeg">
  <source src="project-introduction.ogg" type="audio/ogg">
  <p>Your browser does not support embedded audio.
    <a href="project-introduction.mp3">Download the audio</a>.
  </p>
</audio>
```

- `controls` displays browser-provided playback controls.
- Multiple `<source>` elements allow the browser to choose a supported format.
- Content inside `<audio>` can provide a fallback for browsers that do not support the element.
- `preload` is a hint, not a guarantee: `none` requests no preloading, `metadata` requests basic information, and `auto` allows the browser to decide whether to load more.
- Provide a transcript when spoken content needs an equivalent text representation.
- Avoid autoplaying audio. It can be disruptive and inaccessible.

## 8. Video: `<video>`

The `<video>` element embeds playable video:

```html
<video controls width="960" height="540" preload="metadata" poster="preview.jpg">
  <source src="workflow-demo.mp4" type="video/mp4">
  <source src="workflow-demo.webm" type="video/webm">
  <p>Your browser does not support embedded video.
    <a href="workflow-demo.mp4">Download the video</a>.
  </p>
</video>
```

Useful attributes:

- `controls`: display browser-provided playback controls.
- `width` and `height`: declare the video's intrinsic display dimensions and aspect ratio.
- `poster`: show a preview image before playback.
- `preload`: hint whether media metadata or content should be loaded in advance.
- `muted`: start playback muted when needed for a specific experience.
- `autoplay`: attempts to start playback automatically; browsers may restrict it, and autoplay can disrupt users.
- `loop`: repeat playback automatically.

### Video captions and accessibility

Use a `<track>` element for timed text, such as captions:

```html
<video controls width="960" height="540" poster="preview.jpg">
  <source src="workflow-demo.mp4" type="video/mp4">
  <track
    kind="captions"
    src="workflow-captions-en.vtt"
    srclang="en"
    label="English"
    default>
</video>
```

- Captions provide text for spoken dialogue and important audio information.
- A transcript can provide an additional text alternative.
- Audio description may be needed when important visual information is not conveyed by the soundtrack.
- Provide controls so users can pause, navigate, and adjust playback.
- Do not use autoplay for video with audible sound. Muted autoplay may still be distracting; use it only when appropriate and easy to stop.

## 9. Video controls

The Boolean `controls` attribute exposes the browser's built-in player controls:

```html
<video controls>
  <source src="workflow-demo.mp4" type="video/mp4">
</video>
```

- Controls typically include play/pause, seeking, volume, and fullscreen options, depending on the browser and device.
- If `controls` is omitted, the browser does not have to display the built-in controls. A custom player would then need accessible, keyboard-operable controls and equivalent media functionality.
- For a general-purpose video, native controls are a robust default.
- `controls="false"` does **not** disable controls: Boolean attributes are enabled by their presence. To omit the feature, omit the attribute.

## 10. Embedded content: `<iframe>`

An `<iframe>` embeds another browsing context, commonly a page, map, or video player:

```html
<iframe
  src="https://www.youtube-nocookie.com/embed/VIDEO_ID"
  title="Video: retinal image preprocessing workflow"
  loading="lazy"
  allowfullscreen>
</iframe>
```

Important considerations:

- Give the frame a concise, meaningful `title` so assistive-technology users can identify its content.
- Use a trustworthy, appropriate `src`. An iframe displays content from another origin, which can load scripts and other resources.
- `loading="lazy"` can defer loading an off-screen frame.
- `allowfullscreen` allows fullscreen presentation when supported.
- Use the `sandbox` attribute to restrict embedded content when appropriate. Start with only the permissions the embedded content needs and verify the feature still works. For example, `sandbox="allow-scripts"` is restrictive but may prevent embedded content from navigating or functioning as expected.
- Use the `referrerpolicy` attribute when you need to control referrer information sent with the embedded request.
- Embedding third-party content can affect privacy, performance, and security. Consider consent, trusted providers, and a lightweight preview with an explicit load action.
- Make the iframe responsive with CSS; do not rely on fixed desktop dimensions alone.

```css
.video-frame {
  width: 100%;
  aspect-ratio: 16 / 9;
  border: 0;
}
```

```html
<iframe
  class="video-frame"
  src="https://www.youtube-nocookie.com/embed/VIDEO_ID"
  title="Video: image preprocessing overview"
  loading="lazy"
  allowfullscreen>
</iframe>
```

## Quick comparison

| Requirement | HTML feature |
|---|---|
| Display an image | `<img>` |
| Set image resource | `src` |
| Supply text alternative | `alt` |
| Reserve intrinsic image dimensions | `width` and `height` |
| Offer several image resolutions | `srcset` and `sizes` |
| Select image formats or crops | `<picture>` and `<source>` |
| Group image and caption | `<figure>` and `<figcaption>` |
| Embed audio playback | `<audio>` |
| Embed video playback | `<video>` |
| Show browser player UI | `controls` |
| Add timed text to media | `<track>` |
| Embed another page or player | `<iframe>` |

## Quick interview review

1. **Why is `alt` important?**  
   It supplies a text alternative for meaningful images, supporting screen readers and providing a fallback when an image cannot load.

2. **When should `alt=""` be used?**  
   When an image is decorative and does not add information beyond nearby content.

3. **Why provide image width and height?**  
   The browser can reserve the image's aspect ratio before it loads, reducing layout shifts; CSS can still make the image responsive.

4. **How do `srcset` and `<picture>` differ?**  
   `srcset` gives the browser image candidates, commonly at different resolutions; `<picture>` lets the author specify conditional sources, such as different crops or formats.

5. **How do you make an image responsive?**  
   A common CSS baseline is `max-width: 100%; height: auto;`. For multiple image resources, use `srcset` and `sizes` or `<picture>` as appropriate.

6. **What is the difference between `<figure>` and `<figcaption>`?**  
   `<figure>` groups self-contained content; `<figcaption>` supplies its caption or legend.

7. **How do you add captions to a video?**  
   Use a `<track kind="captions">` resource, commonly a WebVTT file, and provide player controls.

8. **What should you consider when using an iframe?**  
   A meaningful `title`, responsive dimensions, trusted content, loading behavior, and security/privacy constraints such as `sandbox`, where appropriate.

## Good practices to remember

- Write alternative text for the image's purpose in context; use `alt=""` for decorative images.
- Include accurate dimensions and use CSS for responsive display.
- Use `srcset` for resolution choices and `<picture>` for art direction or format choices.
- Add captions or transcripts for media when needed.
- Prefer native audio and video controls unless a custom player is genuinely necessary.
- Do not autoplay disruptive media.
- Label iframes, load them thoughtfully, and limit embedded-content permissions to what is needed.
