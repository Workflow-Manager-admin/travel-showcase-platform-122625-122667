<template>
  <div class="section-layout">
    <div class="section-accent"></div>
    <div class="section-content">
      <slot />
    </div>
  </div>
</template>
<script setup lang="ts">
/** Section layout for travel theme, accent color background material. */
// PUBLIC_INTERFACE
</script>
<style>
.section-layout {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 45vh;
  background: #fff;
  position: relative;
}
.section-accent {
  position: absolute;
  top: 0; left: 50%; transform: translateX(-50%);
  width: 90vw; max-width: 1000px; height: 75px;
  background: linear-gradient(90deg, var(--color-accent), var(--color-primary) 80%);
  border-radius: 0 0 54px 54px/ 0 0 64px 64px;
  z-index: 0;
}
.section-content {
  position: relative;
  z-index: 1;
  margin-top: 55px;
  padding: 3em 2.5em 3em 2.5em;
  background: #fff;
  border-radius: 22px;
  box-shadow: 0 4px 30px #00a5c690;
  text-align: center;
  font-size: 2.5em;
  color: var(--color-primary);
}
</style>
