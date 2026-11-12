<script setup lang="ts">
// A marca: o logo da loja (imagem) ou o nome em letra antiga, com a linha de baixo.
defineProps<{ name: string, tagline?: string, logo?: string }>()
</script>

<template>
  <span class="t-brand">
    <img v-if="logo" class="t-brand__img" :src="logo" :alt="name">
    <span v-else class="t-brand__text">
      <span class="t-brand__name">{{ name }}</span>
      <span v-if="tagline" class="t-brand__tag">{{ tagline }}</span>
    </span>
  </span>
</template>
