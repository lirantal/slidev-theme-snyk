<template>
  <div class="slidev-layout section">
    <div class="section-dots" />
    <div class="section-content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.section-dots {
  position: absolute;
  inset: 0;
  background: url('/bg-dots-purple.png') no-repeat right bottom;
  background-size: 50% auto;
  opacity: 0.25;
  pointer-events: none;
}

.section-content {
  max-width: 700px;
  z-index: 1;
  position: relative;
}
</style>
