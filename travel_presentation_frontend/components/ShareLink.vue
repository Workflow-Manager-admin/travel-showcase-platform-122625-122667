<template>
  <button class="share-link-btn" @click="share" title="Copy presentation link">
    <carbon:share style="margin-right:0.5em;" /> Share Presentation
  </button>
</template>
<script setup lang="ts">
// PUBLIC_INTERFACE
import { ref } from "vue";
/** Share link button for copying presentation url to clipboard. */
function share() {
  window.navigator.clipboard.writeText(window.location.href);
  window.alert("Presentation link copied!");
}
</script>
<style>
.share-link-btn {
  background: var(--color-accent, #50e3c2);
  color: var(--color-primary, #0070f3);
  border: none;
  border-radius: 7px;
  font-size: 1.09em;
  padding: 0.55em 1.4em;
  font-weight: 600;
  cursor: pointer;
  margin-top: 0.7em;
  transition: background 0.15s;
}
.share-link-btn:hover {
  background: var(--color-secondary, #f5a623);
  color: #fff;
}
</style>
