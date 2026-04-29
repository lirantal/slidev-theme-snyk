<template>
  <div class="slidev-layout end">
    <div class="end-content">
      <slot />
    </div>
    <div class="end-logo">
      <img src="/snyk-logo-dark.png" alt="Snyk" class="end-logo-img" />
    </div>
  </div>
</template>

<style scoped>
.end-content {
  z-index: 1;
}

.end-logo {
  position: absolute;
  bottom: 2rem;
  left: 50%;
  transform: translateX(-50%);
  opacity: 0.2;
}

.end-logo-img {
  height: 28px;
  width: auto;
}
</style>
