---
theme: default
layout: custom-theme
title: 🌎 Travel Presentation
cover: https://images.unsplash.com/photo-1468852501093-c15d87773049?auto=format&fit=crop&w=800&q=80
colorSchema:
  accent: "#50e3c2"
  primary: "#0070f3"
  secondary: "#f5a623"
class: text-center
style: |
  :root {
    --color-accent: #50e3c2;
    --color-primary: #0070f3;
    --color-secondary: #f5a623;

    --slidev-theme-background: #f9fafe;
    --slidev-theme-primary: #0070f3;
    --slidev-theme-secondary: #f5a623;
    --slidev-theme-accent: #50e3c2;
    --slidev-theme-navbar: #ffffff;
    --slidev-theme-sidebar: #f4f8fb;
  }
---
layout: center
class: text-center
---

# ✈️ Travel Presentation Maker

Welcome!  
Create, share, and export beautiful travel slideshows.

<template v-if="$slidev.nav.currentPage === 1">
  <img src="https://images.unsplash.com/photo-1506744038136-46273834b3fb?auto=format&fit=crop&w=800&q=80" class="rounded-md shadow-lg mx-auto my-8" style="max-width: 340px;" />
</template>

<div class="mt-8 flex w-full justify-center gap-4">
  <button class="slidev-btn" style="background: var(--color-primary); color: #fff;" @click="$slidev.nav.next">Start Editing <carbon:arrow-right /></button>
</div>

---
layout: custom-editor
class: text-left
---

# 📝 Edit Your First Slide

Edit this slide by clicking the <carbon:edit /> button above.<br>
You can add <span style="color:var(--color-accent)">Text</span>, <span style="color:var(--color-accent)">Images</span>, or <span style="color:var(--color-secondary)">Video</span> below.

- Click the <carbon:add /> button in the sidebar to add slides.
- Drag and drop images onto the slide.
- Embed YouTube videos by pasting links.

<template #footer>
<small>Tip: Use the sidebar to navigate and organize your journey!</small>
</template>

---
layout: image-right
image: https://images.unsplash.com/photo-1512453979798-5ea266f8880c?auto=format&fit=crop&w=800&q=80
class: text-left
---

# 🖼️ Add Images & Video

Just paste the image URL or drag a photo.<br>
To embed a video, paste a YouTube/Vimeo link:

<Youtube id="Lr31FKAur-Q" scale="0.7" />

---
layout: two-cols
class: text-left
---

# 🌍 Sample Destinations

::left::
## Bali

![](https://images.unsplash.com/photo-1501785888041-af3ef285b470?auto=format&fit=crop&w=500&q=80)
- Ubud Rice Terraces
- Tegallalang Swing

::right::
## Paris

![](https://images.unsplash.com/photo-1502602898657-3e91760cbb34?auto=format&fit=crop&w=500&q=80)
- Eiffel Tower
- Louvre Museum

---
layout: section
class: text-center
---

# 🎨 Themes & Layouts

Choose your favorite theme (light/dark/seriph) and layout from the controls in the top bar.<br>
Apply accent color with:  
`theme: default` or `theme: seriph` at the top of this file.

Change slide layout using:
```yaml
layout: image-left
```

---
layout: center
class: text-center
---

# 🔗 Share & Export

- **Share Link:** Click the <carbon:share /> button above to copy a view link.
- **Export PDF:** Use <carbon:document-pdf /> to download slides as PDF.

<div class="mt-4">
  <button class="slidev-btn" style="background:var(--color-secondary);color: #fff;" @click="$slidev.nav.openExport()">Download PDF</button>
  <button class="slidev-btn ml-4" style="background:var(--color-accent);color: #fff;" @click="window.alert('Share your link: '+window.location.href)">Copy Share Link</button>
</div>

---
layout: center
class: text-center
---

# 🚀 Start Your Journey!

Start creating an amazing travel story.  
Use sidebar to add slides, main area to edit, actions above.

Happy exploring!

<style>
.slidev-theme-default,
:root {
  --slidev-theme-background: #f9fafe;
  --slidev-theme-primary: #0070f3;
  --slidev-theme-secondary: #f5a623;
  --slidev-theme-accent: #50e3c2;
}
.slidev-btn {
  border: none;
  padding: 0.8em 2em;
  border-radius: 6px;
  font-weight: bold;
  font-size: 1.1em;
  cursor: pointer;
  margin-top: 1em;
  transition: background 0.2s, color 0.2s;
  box-shadow: 0 2px 8px #0070f340;
}
.slidev-btn:hover {
  opacity: 0.9;
  background: var(--color-accent);
  color: var(--color-primary);
}
.slidev-theme-navbar {
  background: var(--slidev-theme-navbar);
}
.slidev-theme-sidebar {
  background: var(--slidev-theme-sidebar);
}
</style>
