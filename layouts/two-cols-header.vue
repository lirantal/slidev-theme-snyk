<template>
  <div class="slidev-layout two-cols-header">
    <div class="header-area">
      <slot />
    </div>
    <div class="col-left">
      <slot name="left" />
    </div>
    <div class="col-right">
      <slot name="right" />
    </div>
  </div>
</template>

<style scoped>
.header-area {
  grid-column: 1 / -1;
}

.col-left,
.col-right {
  display: flex;
  flex-direction: column;
}
</style>
