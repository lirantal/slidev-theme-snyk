<script setup lang="ts">
interface BarItem {
  label: string
  value: number
  color?: string
  suffix?: string
}

withDefaults(defineProps<{
  data: BarItem[]
  maxValue?: number
  showValues?: boolean
}>(), {
  showValues: true,
})
</script>

<template>
  <div class="bar-chart">
    <div v-for="(item, i) in data" :key="i" class="bar-row">
      <div class="bar-label">{{ item.label }}</div>
      <div class="bar-track">
        <div
          class="bar-fill"
          :style="{
            width: `${(item.value / (maxValue || Math.max(...data.map(d => d.value)))) * 100}%`,
            background: item.color || 'linear-gradient(90deg, var(--snyk-primary), var(--snyk-accent-teal))',
          }"
        />
      </div>
      <div v-if="showValues" class="bar-value">{{ item.value }}{{ item.suffix || '%' }}</div>
    </div>
  </div>
</template>

<style scoped>
.bar-chart {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  width: 100%;
}

.bar-row {
  display: grid;
  grid-template-columns: 140px 1fr 60px;
  align-items: center;
  gap: 0.75rem;
}

.bar-label {
  font-size: 0.85rem;
  color: var(--snyk-text-secondary);
  text-align: right;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
}

.bar-track {
  height: 28px;
  background: var(--snyk-bg-accent);
  border-radius: 6px;
  overflow: hidden;
}

.bar-fill {
  height: 100%;
  border-radius: 6px;
  transition: width 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

.bar-value {
  font-family: 'Sora', sans-serif;
  font-weight: 600;
  font-size: 0.9rem;
  color: var(--snyk-text);
}
</style>
