<template>
  <div class="editor-layout">
    <div class="editor-navbar">
      <slot name="navbar">
        <span class="editor-title">📝 Editor</span>
        <div class="editor-actions">
          <button @click="$slidev.nav.openExport()" title="Export PDF" class="editor-btn"><carbon:document-pdf/> Export</button>
          <button @click="shareLink" title="Share Presentation" class="editor-btn"><carbon:share/> Share</button>
          <button @click="$slidev.nav.addSlide()" title="Add Slide" class="editor-btn"><carbon:add/> Add Slide</button>
        </div>
      </slot>
    </div>
    <div class="editor-main">
      <div class="editor-sidebar">
        <ul>
          <li
            v-for="(slide, idx) in $slidev.nav.slides"
            :key="slide.no"
            :class="{active: idx+1 === $slidev.nav.currentPage}"
            @click="$slidev.nav.go(idx+1)"
          >
            <span>{{ slide.title || ('Slide ' + (idx+1)) }}</span>
            <button v-if="idx+1 === $slidev.nav.currentPage && $slidev.nav.slides.length>1"
              class="editor-delete-btn"
              @click.stop="$slidev.nav.removeSlide(idx+1)"
              title="Delete Slide"
            ><carbon:close /></button>
          </li>
        </ul>
      </div>
      <div class="editor-content">
        <slot/>
        <div class="editor-toolbar mt-6">
          <label>
            <span>Insert Image:</span>
            <input type="file" accept="image/*" style="display:none" @change="onImageUpload"/>
            <button class="editor-btn" @click="$refs.imageInput.click()">Upload</button>
            <input ref="imageInput" type="file" style="display:none" accept="image/*" @change="onImageUpload" />
          </label>
          <label>
            <span>Embed Video (link):</span>
            <input v-model="newVideo" placeholder="https://youtube.com/..." style="width:200px;"/>
            <button class="editor-btn" @click="insertVideo">Insert</button>
          </label>
          <label>
            <span>Theme:</span>
            <select v-model="theme" @change="changeTheme">
              <option value="default">Modern Light</option>
              <option value="seriph">Seriph</option>
              <option value="dark">Dark</option>
            </select>
          </label>
        </div>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
// PUBLIC_INTERFACE
import { ref } from 'vue';
/** Layout component for central editing area in Slidev, with sidebar, topbar, and media-insert controls. */
const theme = ref('default');
const newVideo = ref('');

function onImageUpload(e: Event) {
  const files = (e.target as HTMLInputElement).files;
  if (files && files[0]) {
    const reader = new FileReader();
    reader.onload = function(ev) {
      // Insert Markdown image at cursor (or at slide)
      const md = `![](${ev.target?.result})`;
      document.execCommand('insertText', false, md);
    };
    reader.readAsDataURL(files[0]);
  }
}

function insertVideo() {
  if (newVideo.value) {
    // Insert Youtube component markdown
    const vidUrl = newVideo.value.trim();
    // Automatically detect Youtube
    let id = '';
    if (vidUrl.includes('youtu')) {
      id = vidUrl.split(/v=|\/embed\/|\/youtu\.be\/|\/shorts\//).pop().split(/[?& ]/)[0];
    }
    if (id.length) {
      const snippet = `<Youtube id="${id}" />`
      document.execCommand('insertText', false, snippet + '\n');
    }
    newVideo.value = '';
  }
}

function changeTheme() {
  $slidev.config.theme = theme.value
}

function shareLink() {
  window.navigator.clipboard.writeText(window.location.href);
  window.alert('Shareable link copied!');
}
</script>
<style>
.editor-layout { display: flex; flex-direction: column; height: 100vh; }
.editor-navbar {
  background: var(--color-primary);
  color: #fff;
  display: flex;
  align-items: center;
  gap: 1em;
  padding: 0.6em 2em;
  min-height: 54px;
  font-size: 1.12em;
  font-weight: bold;
  box-shadow: 0 1px 4px #0070f320;
}
.editor-title { flex: 1; }
.editor-actions { display: flex; gap: 0.5em; }
.editor-btn {
  background: var(--color-secondary);
  border: none;
  color: #fff;
  padding: 0.5em 1.1em;
  margin-left: 0.5em;
  font-size: 1em;
  border-radius: 5px;
  cursor: pointer;
  transition: background 0.17s;
}
.editor-btn:hover {
  background: var(--color-accent);
  color: var(--color-primary);
}
.editor-main { display: flex; flex: 1 1 auto; min-height: 0; }
.editor-sidebar {
  background: var(--color-accent, #50e3c2);
  width: 160px;
  min-width: 140px;
  max-width: 220px;
  padding: 1.1em 0.1em;
  box-shadow: 2px 0 8px #8881;
}
.editor-sidebar ul {
  list-style: none;
  margin: 0; padding: 0;
}
.editor-sidebar li {
  background: rgba(255,255,255,0.97);
  border-radius: 6px;
  margin: 0.2em 0.5em;
  padding: 0.7em 0.9em;
  cursor: pointer;
  color: #25686c;
  font-weight: 500;
  display: flex;
  align-items: center;
  justify-content: space-between;
  transition: box-shadow 0.15s;
}
.editor-sidebar li.active, .editor-sidebar li:hover {
  background: var(--color-secondary, #f5a623);
  color: #fff;
  box-shadow: 0 2px 10px #f5a62330;
}
.editor-delete-btn {
  background: transparent;
  border: none;
  color: #a54545;
  font-size: 1.18em;
  padding: 0 0 0 0.4em;
  cursor: pointer;
}
.editor-content {
  flex: 1;
  padding: 3em 2.4em;
  background: #fff;
  border-radius: 16px;
  margin: 2em 1.4em 2em 2.2em;
  box-shadow: 0 4px 38px #2221;
  min-height: 400px;
}
.editor-toolbar {
  display: flex;
  row-gap: 0.4em;
  column-gap: 1em;
  flex-wrap: wrap;
  margin-top: 1.2em;
  align-items: center;
  font-size: 1.03em;
}
.editor-toolbar input[type='text'],
.editor-toolbar input[type='url'] {
  padding: 0.20em 0.8em;
  border-radius: 5px;
  border: 1px solid #aaa;
}
.editor-toolbar select {
  padding: 0.18em 0.6em;
  border-radius: 5px;
  border: 1.5px solid #bbb;
}
</style>
