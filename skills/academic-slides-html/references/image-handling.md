# Image Handling Guide

This guide addresses the common problem of "text-only" slides by providing a complete image processing workflow.

## The Problem

Most LLM-generated presentations are text-only because:
1. Images are lost during PDF/docx text extraction
2. LLM cannot locate extracted images
3. Office tools make image insertion difficult

## The Solution

HTML + base64 embedding enables fully self-contained slides with images.

## Workflow

### Phase 1: Image Discovery

Before generating slides, identify all figures and tables in the source document.

**Input:** Markdown document with figure references

**Process:**
1. Scan for figure/table references (e.g., "Figure 1", "Table 2", "Fig. 3")
2. Extract captions (text near the reference)
3. Note location in document (section, paragraph)

**Output:** Image manifest

```markdown
| ID | Type | Caption | Location |
|----|------|---------|----------|
| 1 | Figure | Architecture of proposed method | Section 3.1 |
| 2 | Table | Comparison with baselines | Section 4.2 |
| 3 | Figure | Training loss curves | Section 4.1 |
```

### Phase 2: Image Extraction

If source is PDF, extract the actual images.

**Tool options:**

#### Option 1: PyMuPDF (Python)

```python
import fitz  # pymupdf

def extract_images(pdf_path, output_dir):
    doc = fitz.open(pdf_path)
    for page_num in range(len(doc)):
        page = doc[page_num]
        images = page.get_images(full=True)
        for img_idx, img in enumerate(images):
            xref = img[0]
            base_image = doc.extract_image(xref)
            image_bytes = base_image["image"]
            # Save image
            with open(f"{output_dir}/page{page_num+1}_img{img_idx+1}.png", "wb") as f:
                f.write(image_bytes)
```

#### Option 2: pdf2image

```python
from pdf2image import convert_from_path

images = convert_from_path('paper.pdf', dpi=200)
for i, image in enumerate(images):
    image.save(f'page_{i+1}.png', 'PNG')
```

#### Option 3: Manual extraction

If automatic extraction fails, ask user to:
1. Open PDF in a viewer
2. Screenshot or save each figure
3. Provide as separate image files

### Phase 3: Image Assignment

Map figures to slides based on narrative flow.

**Principles:**

1. **Architecture/method figures** → Method section slides
2. **Result tables/charts** → Results section slides
3. **Comparison figures** → Related work or results slides
4. **Supplementary figures** → Backup slides or omit

**Decision framework:**

```
For each figure:
  1. What does it illustrate?
  2. Which slide's argument does it support?
  3. Is it essential or supplementary?
  
Assign to the slide where it:
- Introduces a concept (before the explanation)
- Supports a claim (alongside the text)
- Shows evidence (in results section)
```

### Phase 4: Base64 Embedding

Convert images to base64 for self-contained HTML.

**Python conversion:**

```python
import base64

def image_to_base64(image_path):
    with open(image_path, "rb") as image_file:
        encoded_string = base64.b64encode(image_file.read()).decode()
    return f"data:image/png;base64,{encoded_string}"
```

**Usage in HTML:**

```html
<img src="data:image/png;base64,iVBORw0KGgo..." alt="Figure 1: Architecture">
```

**JavaScript conversion (if needed):**

```javascript
// For browser-side conversion
function imageToBase64(file) {
  return new Promise((resolve, reject) => {
    const reader = new FileReader();
    reader.onload = () => resolve(reader.result);
    reader.onerror = reject;
    reader.readAsDataURL(file);
  });
}
```

## Image Quality Guidelines

| Use Case | Resolution | Format |
|----------|------------|--------|
| Architecture diagrams | High (300 DPI) | PNG |
| Charts/plots | Medium (200 DPI) | PNG |
| Photos | Medium (150 DPI) | JPEG |
| Tables | High (300 DPI) | PNG |

## Troubleshooting

### Images not extracting from PDF

- PDF may use scanned images → use OCR + extraction
- Vector graphics → may need screenshot
- Complex layouts → manual extraction

### Base64 too large

- Compress images before encoding
- Reduce resolution if acceptable
- Use JPEG for photos (smaller than PNG)

### Figures misidentified

- Cross-reference with text mentions
- Check figure numbers in captions
- Verify with user if uncertain

## Example Integration

```python
# Complete workflow example
import fitz
import base64

def process_paper_figures(pdf_path):
    # Step 1: Extract images
    doc = fitz.open(pdf_path)
    figures = []
    
    for page_num in range(len(doc)):
        page = doc[page_num]
        images = page.get_images(full=True)
        
        for img_idx, img in enumerate(images):
            xref = img[0]
            base_image = doc.extract_image(xref)
            
            # Step 2: Convert to base64
            image_bytes = base_image["image"]
            b64_string = base64.b64encode(image_bytes).decode()
            
            figures.append({
                "page": page_num + 1,
                "index": img_idx + 1,
                "base64": f"data:image/png;base64,{b64_string}",
                "format": base_image["ext"]
            })
    
    return figures
```
