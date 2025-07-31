<template>
  <button class="pdf-export-btn" @click="$slidev.nav.openExport()" title="Download PDF">
    <carbon:document-pdf style="margin-right:0.5em;" />Export as PDF
  </button>
</template>
<script setup lang="ts">
// PUBLIC_INTERFACE
/** Button for triggering Slidev PDF export. */
</script>
<style>
.pdf-export-btn {
  background: var(--color-secondary, #f5a623);
  color: #fff;
  border: none;
  border-radius: 7px;
  font-size: 1.09em;
  padding: 0.55em 1.4em;
  font-weight: 600;
  cursor: pointer;
  margin-top: 0.7em;
  transition: background 0.15s;
}
.pdf-export-btn:hover {
  background: var(--color-accent, #50e3c2);
  color: var(--color-primary, #0070f3);
}
</style>
