<script setup lang="ts">
// A mandala de raios dourados (a do site da Bruxa): fundo decorativo.
const props = withDefaults(defineProps<{ rays?: number }>(), { rays: 48 })
const lines = computed(() => Array.from({ length: props.rays }, (_, k) => {
  const i = k + 1
  const a = (i / props.rays) * 2 * Math.PI
  return { i, x: 100 + 95 * Math.cos(a), y: 100 + 95 * Math.sin(a), o: i % 2 === 0 ? 0.9 : 0.4 }
}))
</script>

<template>
  <svg viewBox="0 0 200 200" fill="none" aria-hidden="true">
    <g stroke="currentColor" stroke-width="0.6">
      <line v-for="l in lines" :key="l.i" x1="100" y1="100" :x2="l.x" :y2="l.y" :opacity="l.o" />
    </g>
    <circle cx="100" cy="100" r="60" stroke="currentColor" stroke-width="0.8" opacity="0.5" />
    <circle cx="100" cy="100" r="46" stroke="currentColor" stroke-width="0.8" opacity="0.7" />
    <circle cx="100" cy="100" r="10" fill="currentColor" opacity="0.8" />
  </svg>
</template>
