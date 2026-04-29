<template>
  <div class="slidev-layout quote">
    <div class="quote-content">
      <slot />
    </div>
  </div>
</template>

<style scoped>
.quote-content {
  max-width: 700px;
  position: relative;
  z-index: 1;
}
</style>
