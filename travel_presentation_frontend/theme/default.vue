<template>
  <div class="slidev-theme-default-root">
    <header class="slidev-theme-navbar">
      <slot name="navbar">
        <div class="navbar-inner">
          <img src="https://svgshare.com/i/yMu.svg" class="logo" alt="Travel Logo" />
          <span class="title">{{ $slidev.config.title || "Travel Presentation" }}</span>
          <div class="nav-actions">
            <button class="nav-btn" @click="$slidev.nav.openExport()" title="Export PDF">
              <carbon:document-pdf />
            </button>
            <button class="nav-btn" @click="copyLink" title="Share Link">
              <carbon:share />
            </button>
            <button class="nav-btn" @click="$slidev.nav.openInEditor()" title="Edit Slides">
              <carbon:edit />
            </button>
          </div>
        </div>
      </slot>
    </header>
    <main class="slidev-theme-main">
      <aside class="slidev-theme-sidebar">
        <slot name="sidebar">
          <div class="sidebar-header">
            <carbon:list />
            <span>Slides</span>
            <button class="sidebar-btn" @click="addSlide" title="Add Slide">
              <carbon:add />
            </button>
          </div>
          <ul class="sidebar-thumbnails">
            <li
              v-for="(slide, idx) in $slidev.nav.slides"
              :key="slide.no"
              :class="{ active: idx + 1 === $slidev.nav.currentPage }"
              @click="$slidev.nav.go(idx+1)"
            >
              <span class="slide-thumb-number">{{ idx + 1 }}</span>
              <span class="slide-thumb-title">{{ slide.title || ('Slide ' + (idx+1)) }}</span>
            </li>
          </ul>
        </slot>
      </aside>
      <section class="slidev-theme-content">
        <slot />
      </section>
    </main>
  </div>
</template>

<script setup lang="ts">
// PUBLIC_INTERFACE
import { ref } from "vue";
/** Theme root component for Slidev with modern light colors, sidebar, navbar, and responsive design. */

function copyLink() {
  window.navigator.clipboard.writeText(window.location.href)
}
function addSlide() {
  $slidev.nav.addSlide();
}
</script>

<style>
.slidev-theme-default-root {
  background: var(--slidev-theme-background, #f9fafe);
  color: #2d3748;
  min-height: 100vh;
  font-family: 'Inter', 'Segoe UI', sans-serif;
  display: flex;
  flex-direction: column;
}
.slidev-theme-navbar {
  background: var(--slidev-theme-navbar, #fff);
  border-bottom: 2px solid var(--color-primary);
  padding: 0.4em 2.2em;
  min-height: 54px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  z-index: 5;
}
.navbar-inner {
  display: flex;
  width: 100%;
  align-items: center;
  gap: 1.2em;
}
.logo {
  width: 36px; height: 36px; margin-right: 8px;
}
.title {
  color: var(--color-primary);
  font-size: 1.3em;
  font-weight: bold;
  flex: 1;
  letter-spacing: 1px;
}
.nav-actions {
  display: flex;
  gap: 0.4em;
}
.nav-btn {
  background: none;
  border: none;
  font-size: 1.2em;
  padding: 0.3em 0.5em;
  color: var(--color-primary);
  cursor: pointer;
  border-radius: 3px;
  transition: background 0.15s, color 0.15s;
}
.nav-btn:hover {
  background: var(--color-accent);
  color: #fff;
}
.slidev-theme-main {
  display: flex;
  flex: 1 1 auto;
  min-height: 0;
}
.slidev-theme-sidebar {
  background: var(--slidev-theme-sidebar, #f4f8fb);
  width: 250px;
  min-width: 210px;
  max-width: 300px;
  height: 100vh;
  box-shadow: 2px 0 8px #ddd3;
  border-right: 1.5px solid var(--color-accent);
  display: flex;
  flex-direction: column;
}
.sidebar-header {
  display: flex;
  align-items: center;
  gap: 0.4em;
  font-size: 1.08em;
  color: var(--color-secondary);
  padding: 1.2em 0.8em 0.4em 1.1em;
  font-weight: 500;
}
.sidebar-btn {
  margin-left: auto;
  background: var(--color-accent);
  border: none;
  border-radius: 5px;
  color: #fff;
  font-size: 1.08em;
  padding: 0.27em 0.8em;
  cursor: pointer;
  transition: background 0.17s;
}
.sidebar-btn:hover {
  background: var(--color-primary);
}
.sidebar-thumbnails {
  flex: 1 1 auto;
  padding: 0 0.8em 0.4em 0.8em;
  list-style: none;
  margin: 0;
  overflow-y: auto;
}
.sidebar-thumbnails li {
  display: flex;
  gap: 0.7em;
  align-items: center;
  background: transparent;
  font-size: 1.05em;
  border-radius: 4px;
  margin: 0.1em 0;
  padding: 0.4em 0.8em;
  cursor: pointer;
  color: #333;
  transition: background 0.16s, color 0.11s;
}
.sidebar-thumbnails li.active,
.sidebar-thumbnails li:hover {
  background: var(--color-accent);
  color: #fff;
  font-weight: bold;
}
.slide-thumb-number {
  background: var(--color-primary);
  color: #fff;
  border-radius: 50%;
  font-size: 0.93em;
  width: 1.52em;
  height: 1.52em;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  margin-right: 0.2em;
}
.slide-thumb-title {
  flex: 1;
  text-overflow: ellipsis;
  overflow: hidden;
  white-space: nowrap;
  font-weight: 500;
}
.slidev-theme-content {
  flex: 1 1 auto;
  min-width: 0;
  min-height: 0;
  padding: 1.6em 2.5em 2.4em 2.5em;
  background: var(--slidev-theme-background, #f9fafe);
  display: flex;
  flex-direction: column;
  border-radius: 18px;
  margin: 1.7em 2.5em 1.7em 0;
  box-shadow: 0 2px 40px #0070f329;
}
@media (max-width: 900px) {
  .slidev-theme-sidebar { display: none; }
  .slidev-theme-content { margin: 4vw 2vw 4vw 2vw; }
}
</style>
