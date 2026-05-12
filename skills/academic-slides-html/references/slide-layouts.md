# Slide Layout Patterns

## Title Slide

```html
<section class="slide slide-title">
  <div class="slide-content" style="justify-content: center; align-items: center; text-align: center;">
    <h1>{Paper Title}</h1>
    <p class="subtitle" style="font-size: 1.2em; color: #666;">{Subtitle if any}</p>
    <p style="margin-top: 2em;">{Author 1}, {Author 2}, ...</p>
    <p style="color: #666;">{Affiliation}</p>
    <p style="margin-top: 1em; color: #888;">{Conference Name} {Year}</p>
  </div>
</section>
```

## Content Slide (Text + Bullet Points)

```html
<section class="slide">
  <div class="slide-content">
    <h2>{Slide Title as Claim}</h2>
    <ul>
      <li>{Point 1}</li>
      <li>{Point 2}</li>
      <li>{Point 3}</li>
    </ul>
  </div>
</section>
```

## Figure Slide (Single Image Focus)

```html
<section class="slide">
  <div class="slide-content">
    <h2>{Figure Title}</h2>
    <img class="slide-image" src="data:image/png;base64,{base64}" alt="{caption}">
    <p class="figure-caption">Figure {N}: {Caption}</p>
  </div>
</section>
```

## Two-Column Slide (Text + Figure)

```html
<section class="slide">
  <div class="slide-content">
    <h2>{Slide Title}</h2>
    <div class="two-columns">
      <div>
        <ul>
          <li>{Point 1}</li>
          <li>{Point 2}</li>
          <li>{Point 3}</li>
        </ul>
      </div>
      <div>
        <img class="slide-image" src="data:image/png;base64,{base64}" alt="{caption}">
        <p class="figure-caption">{Caption}</p>
      </div>
    </div>
  </div>
</section>
```

## Comparison Slide

```html
<section class="slide">
  <div class="slide-content">
    <h2>{Comparison Title}</h2>
    <div class="two-columns">
      <div>
        <h3>{Approach A}</h3>
        <ul>
          <li>{Characteristic 1}</li>
          <li>{Characteristic 2}</li>
        </ul>
      </div>
      <div>
        <h3>{Approach B}</h3>
        <ul>
          <li>{Characteristic 1}</li>
          <li>{Characteristic 2}</li>
        </ul>
      </div>
    </div>
  </div>
</section>
```

## Key Point Slide (Single Message)

```html
<section class="slide">
  <div class="slide-content" style="justify-content: center; align-items: center;">
    <p class="key-point">{One key takeaway}</p>
  </div>
</section>
```

## Results Slide (Table or Chart)

```html
<section class="slide">
  <div class="slide-content">
    <h2>{Results Title}</h2>
    <table style="width: 100%; border-collapse: collapse; margin-top: 1em;">
      <thead>
        <tr>
          <th style="border-bottom: 2px solid #333; padding: 0.5em; text-align: left;">{Header 1}</th>
          <th style="border-bottom: 2px solid #333; padding: 0.5em; text-align: left;">{Header 2}</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td style="border-bottom: 1px solid #ddd; padding: 0.5em;">{Data}</td>
          <td style="border-bottom: 1px solid #ddd; padding: 0.5em;">{Data}</td>
        </tr>
      </tbody>
    </table>
  </div>
</section>
```

## Section Divider

```html
<section class="slide" style="background: #2c3e50; color: white;">
  <div class="slide-content" style="justify-content: center; align-items: center; text-align: center;">
    <h2 style="color: white; border: none;">{Section Title}</h2>
  </div>
</section>
```

## Method/Architecture Slide

```html
<section class="slide">
  <div class="slide-content">
    <h2>Method Overview</h2>
    <img class="slide-image" src="data:image/png;base64,{base64}" alt="Architecture diagram">
    <p class="figure-caption">Figure {N}: System architecture</p>
  </div>
</section>
```

## Q&A Slide

```html
<section class="slide" style="background: #2c3e50; color: white;">
  <div class="slide-content" style="justify-content: center; align-items: center; text-align: center;">
    <h1 style="color: white;">Thank You</h1>
    <p style="margin-top: 1em; font-size: 1.5em;">Q&A</p>
  </div>
</section>
```

## Layout Selection Guide

| Content Type | Recommended Layout |
|--------------|-------------------|
| Opening | Title slide |
| Motivation/Problem | Key point or text |
| Related work | Comparison or text |
| Method overview | Figure (architecture) |
| Method details | Two-column (text + figure) |
| Experiments setup | Text or table |
| Results | Figure or table |
| Analysis | Two-column or figure |
| Conclusion | Key point or text |
| Closing | Q&A slide |
