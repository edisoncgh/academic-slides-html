# HTML Template and CSS Specifications

## HTML Structure

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>{Presentation Title}</title>
  <style>
    /* CSS goes here */
  </style>
</head>
<body>
  <div class="slides-container">
    <!-- Slide 1: Title -->
    <section class="slide slide-title">
      <div class="slide-content">
        <h1>{Title}</h1>
        <p class="subtitle">{Subtitle}</p>
        <p class="author">{Author}, {Affiliation}</p>
        <p class="venue">{Conference/Date}</p>
      </div>
    </section>

    <!-- Slide 2: Content -->
    <section class="slide">
      <div class="slide-content">
        <h2>{Slide Title}</h2>
        <!-- Content varies by layout -->
      </div>
    </section>

    <!-- More slides... -->
  </div>
</body>
</html>
```

## CSS Base

```css
/* Reset and base */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Times New Roman", "SimSun", serif;
  background: #f5f5f5;
  color: #333;
}

/* Slides container - scroll snap */
.slides-container {
  scroll-snap-type: y mandatory;
  overflow-y: scroll;
  height: 100vh;
}

/* Individual slide */
.slide {
  scroll-snap-align: start;
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  background: white;
  position: relative;
}

/* 16:9 content area */
.slide-content {
  width: 80%;
  max-width: 1200px;
  aspect-ratio: 16 / 9;
  padding: 4% 5%;
  display: flex;
  flex-direction: column;
}

/* Typography */
h1 {
  font-size: 2.5em;
  font-weight: bold;
  margin-bottom: 0.5em;
}

h2 {
  font-size: 1.8em;
  font-weight: bold;
  margin-bottom: 0.8em;
  border-bottom: 2px solid #2c3e50;
  padding-bottom: 0.3em;
}

h3 {
  font-size: 1.3em;
  font-weight: bold;
  margin-bottom: 0.5em;
}

p, li {
  font-size: 1.1em;
  line-height: 1.6;
}

ul, ol {
  margin-left: 1.5em;
  margin-bottom: 1em;
}

/* Images */
.slide-image {
  max-width: 100%;
  max-height: 70vh;
  object-fit: contain;
  margin: 1em auto;
  display: block;
}

.figure-caption {
  text-align: center;
  font-size: 0.9em;
  color: #666;
  margin-top: 0.5em;
}

/* Special elements */
.highlight {
  background: #fff3cd;
  padding: 0.2em 0.4em;
  border-radius: 3px;
}

.key-point {
  font-size: 1.3em;
  font-weight: bold;
  color: #2c3e50;
  text-align: center;
  margin: 1em 0;
}

/* Two-column layout */
.two-columns {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 2em;
}

/* Footer */
.slide-number {
  position: absolute;
  bottom: 1em;
  right: 1.5em;
  font-size: 0.8em;
  color: #999;
}
```

## Responsive Behavior

For mobile viewing while maintaining PPT feel:

```css
@media (max-width: 768px) {
  .slide-content {
    width: 95%;
    padding: 3%;
  }

  h1 { font-size: 1.8em; }
  h2 { font-size: 1.4em; }
  p, li { font-size: 0.95em; }

  .two-columns {
    grid-template-columns: 1fr;
  }
}
```

## Color Palette (Academic)

| Element | Color | Usage |
|---------|-------|-------|
| Primary text | `#333333` | Body text |
| Headings | `#2c3e50` | h1, h2, h3 |
| Accent | `#3498db` | Links, highlights |
| Background | `#ffffff` | Slide background |
| Light gray | `#f8f9fa` | Alternate slides |
| Border | `#dee2e6` | Dividers |

## Slide Numbering

Add slide numbers via CSS counter:

```css
.slides-container {
  counter-reset: slide-counter;
}

.slide {
  counter-increment: slide-counter;
}

.slide::after {
  content: counter(slide-counter);
  position: absolute;
  bottom: 1em;
  right: 1.5em;
  font-size: 0.8em;
  color: #999;
}
```
