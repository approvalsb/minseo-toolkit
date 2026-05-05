---
name: guide-mode
description: Inject a UX/UI Guide Mode overlay into any HTML page. Use when the user wants to inspect, annotate, or understand the design structure of a webpage — shows component names, dimensions, font sizes, padding, and CSS class info on hover. Invoke with "/guide-mode [file path or URL]".
license: MIT
---

This skill injects a **Guide Mode** toggle into any static HTML page, enabling an interactive design inspection overlay. When activated, hovering over any element reveals its component name (Korean + English), dimensions, font size, and padding — like a lightweight browser DevTools for designers and non-developers.

## When to Use

- User says "가이드모드", "guide mode", "디자인 검사", "컴포넌트 확인"
- User wants to understand or annotate page structure
- UX/UI review, design handoff, or onboarding scenarios

## Implementation Steps

### 1. Identify Target File

- If a file path is given, read that HTML file
- If a URL is given, find the corresponding local HTML file in the project
- If neither, ask the user which page to annotate

### 2. Analyze Page Structure

Read the HTML and CSS files. Build a label map by scanning:

- **Semantic tags**: `nav`, `header`, `main`, `section`, `footer`, `aside`, `article`
- **CSS class names**: Match known patterns (e.g., `.hero`, `.cta`, `.card`, `.grid`, `.btn`)
- **ARIA roles and landmarks**
- **Component nesting hierarchy**

Generate a `labels` object mapping CSS selectors to bilingual descriptions:

```javascript
// Format: 'selector': 'English Name (한국어명) — description'
{
  'nav': 'Nav Bar (네비게이션 바) — 상단 메뉴',
  '.hero': 'Hero Section (히어로) — 첫 화면 대형 섹션',
  '.btn': 'Button (버튼) — 클릭 요소',
  // ... auto-generated from actual page structure
}
```

### 3. Inject Guide Mode Code

Insert the following block **before `</body>`** in the target HTML file. Adapt the `labels` object to match the actual page structure.

```html
<!-- UX/UI Guide Mode -->
<button id="guide-toggle" style="position:fixed;bottom:20px;right:20px;z-index:9999;padding:10px 16px;background:#1A2744;color:#fff;border:none;border-radius:100px;font-size:12px;font-weight:600;cursor:pointer;box-shadow:0 4px 16px rgba(0,0,0,.2);font-family:system-ui,sans-serif;transition:all .2s" onclick="document.body.classList.toggle('guide-on');this.textContent=document.body.classList.contains('guide-on')?'Guide ON':'Guide Mode'">Guide Mode</button>
<div id="guide-tooltip" style="position:fixed;z-index:9998;padding:10px 16px;background:rgba(26,39,68,.95);color:#fff;border-radius:10px;font-size:12px;font-weight:500;pointer-events:none;opacity:0;transition:opacity .15s;font-family:system-ui,sans-serif;white-space:pre;box-shadow:0 4px 12px rgba(0,0,0,.2);line-height:1.6;max-width:360px"></div>
<style>
  .guide-on *{transition:outline .1s!important}
  .guide-on [data-guide]:hover{outline:2px solid #00FF66!important;outline-offset:2px;cursor:help;box-shadow:0 0 8px rgba(0,255,102,.3)!important}
  .guide-on #guide-toggle{background:#C19A5B;color:#1A2744}
</style>
<script>
(function(){
  const labels = {/* REPLACE: auto-generated label map */};

  // Apply data-guide attributes
  Object.keys(labels).forEach(function(sel){
    document.querySelectorAll(sel).forEach(function(el){
      el.setAttribute('data-guide', labels[sel]);
    });
  });

  // Tooltip logic
  var tip = document.getElementById('guide-tooltip');
  document.addEventListener('mousemove', function(e){
    if(!document.body.classList.contains('guide-on')) return;
    var t = e.target.closest('[data-guide]');
    if(t){
      var r = t.getBoundingClientRect();
      var w = Math.round(r.width);
      var h = Math.round(r.height);
      var cs = getComputedStyle(t);
      var fs = cs.fontSize;
      var pt = cs.paddingTop, pb = cs.paddingBottom, pl = cs.paddingLeft, pr = cs.paddingRight;
      var info = t.getAttribute('data-guide');
      info += '\n' + w + ' x ' + h + 'px';
      if(parseFloat(fs) > 0) info += '  |  font: ' + fs;
      var pad = [];
      if(parseFloat(pt) > 0 || parseFloat(pb) > 0) pad.push(pt + ' / ' + pb);
      if(parseFloat(pl) > 0 || parseFloat(pr) > 0) pad.push(pl + ' / ' + pr);
      if(pad.length) info += '\npadding: ' + pad.join(' , ');
      // Show CSS classes
      var cls = t.className;
      if(typeof cls === 'string' && cls.trim()) info += '\nclass: .' + cls.trim().split(/\s+/).join(' .');
      tip.textContent = info;
      tip.style.opacity = '1';
      tip.style.left = Math.min(e.clientX + 14, window.innerWidth - tip.offsetWidth - 20) + 'px';
      tip.style.top = Math.max(e.clientY - tip.offsetHeight - 10, 8) + 'px';
    } else {
      tip.style.opacity = '0';
    }
  });
})();
</script>
<!-- /UX/UI Guide Mode -->
```

### 4. Label Generation Rules

When building the `labels` map, follow these conventions:

| Pattern | Label Format |
|---------|-------------|
| `nav`, `.nav*` | Nav Bar (네비게이션 바) |
| `.hero*` | Hero Section (히어로) |
| `.btn*`, `button` | Button (버튼) + variant |
| `.card*`, `.sc` | Card (카드) |
| `.grid*`, `.sg` | Grid Layout (그리드) |
| `h1`~`h6` | Heading / H{n} (헤딩) |
| `.cta*` | CTA (콜투액션) |
| `footer`, `.footer*` | Footer (푸터) |
| `.label`, `.eyebrow` | Label (라벨) — 섹션 소제목 |
| `section`, `.sec*` | Section (섹션) + context |
| `.modal*`, `.dialog*` | Modal (모달) |
| `form`, `.form*` | Form (폼) |
| `input`, `textarea`, `select` | Input (입력 필드) |
| `.accordion*`, `details` | Accordion (아코디언) |
| `.tab*` | Tab (탭) |
| `.badge*`, `.tag*` | Badge (뱃지) |
| `.avatar*` | Avatar (아바타) |
| `.breadcrumb*` | Breadcrumb (브레드크럼) |
| `img`, `.img*` | Image (이미지) + alt text |

- Always include both English and Korean names
- Add contextual descriptions based on content (e.g., "Service Card (서비스 카드) — 12개 서비스 그리드")
- For nested elements, describe their role within the parent (e.g., "Card Title (카드 제목)")
- Include layout info for containers (e.g., "Grid Layout (그리드) — 4열 배치")

### 5. Customization

Adapt the Guide Mode colors to match the page's design system:

- **Toggle button**: Use the page's primary dark color
- **Active state**: Use the page's accent color
- **Outline color**: Keep `#00FF66` (high contrast, visible on any background)
- **Tooltip**: Dark semi-transparent background for readability

### 6. Removal

When the user says "가이드모드 제거" or "remove guide mode":
- Remove everything between `<!-- UX/UI Guide Mode -->` and `<!-- /UX/UI Guide Mode -->`
- Clean up any `data-guide` attributes if they were baked into the HTML

## Output

After injection, inform the user:
- Guide Mode toggle button is at the bottom-right corner
- Click to enable/disable
- Hover over any element to see component info
- The overlay is development-only — remove before production deploy
