<script setup lang="ts">
interface CompareItem {
  label: string
  valueA: number
  valueB: number
  suffix?: string
}

withDefaults(defineProps<{
  data: CompareItem[]
  labelA?: string
  labelB?: string
  colorA?: string
  colorB?: string
  maxValue?: number
}>(), {
  labelA: 'Before',
  labelB: 'After',
  colorA: 'var(--snyk-text-muted)',
  colorB: 'var(--snyk-accent-teal)',
})
</script>

<template>
  <div class="comparison-chart">
    <div class="comparison-legend">
      <span class="legend-item"><span class="legend-dot" :style="{ background: colorA }" /> {{ labelA }}</span>
      <span class="legend-item"><span class="legend-dot" :style="{ background: colorB }" /> {{ labelB }}</span>
    </div>
    <div v-for="(item, i) in data" :key="i" class="compare-row">
      <div class="compare-label">{{ item.label }}</div>
      <div class="compare-bars">
        <div class="compare-track">
          <div class="compare-fill" :style="{ width: `${(item.valueA / (maxValue || 100)) * 100}%`, background: colorA }" />
        </div>
        <div class="compare-track">
          <div class="compare-fill" :style="{ width: `${(item.valueB / (maxValue || 100)) * 100}%`, background: colorB }" />
        </div>
      </div>
      <div class="compare-values">
        <span>{{ item.valueA }}{{ item.suffix || '%' }}</span>
        <span class="compare-value-highlight">{{ item.valueB }}{{ item.suffix || '%' }}</span>
      </div>
    </div>
  </div>
</template>

<style scoped>
.comparison-chart {
  width: 100%;
}

.comparison-legend {
  display: flex;
  gap: 1.5rem;
  margin-bottom: 1rem;
  font-size: 0.8rem;
  color: var(--snyk-text-secondary);
}

.legend-item {
  display: flex;
  align-items: center;
  gap: 0.4rem;
}

.legend-dot {
  width: 10px;
  height: 10px;
  border-radius: 3px;
}

.compare-row {
  display: grid;
  grid-template-columns: 120px 1fr 80px;
  align-items: center;
  gap: 0.75rem;
  margin-bottom: 0.6rem;
}

.compare-label {
  font-size: 0.85rem;
  color: var(--snyk-text-secondary);
  text-align: right;
}

.compare-bars {
  display: flex;
  flex-direction: column;
  gap: 3px;
}

.compare-track {
  height: 14px;
  background: var(--snyk-bg-accent);
  border-radius: 4px;
  overflow: hidden;
}

.compare-fill {
  height: 100%;
  border-radius: 4px;
  transition: width 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

.compare-values {
  display: flex;
  flex-direction: column;
  font-size: 0.75rem;
  color: var(--snyk-text-muted);
  gap: 1px;
}

.compare-value-highlight {
  color: var(--snyk-accent-teal);
  font-weight: 600;
}
</style>
