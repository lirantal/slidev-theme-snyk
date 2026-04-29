<template>
  <div class="slidev-layout two-cols">
    <div class="col-left">
      <slot />
    </div>
    <div class="col-right">
      <slot name="right" />
    </div>
  </div>
</template>

<style scoped>
.col-left,
.col-right {
  display: flex;
  flex-direction: column;
  justify-content: center;
}
</style>
