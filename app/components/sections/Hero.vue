<script setup lang="ts">
// Abertura da Bruxa: a mandala dourada com o titulo numa faixa de ouro. Com foto,
// a foto fica ao lado; sem foto, so a mandala no centro.
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
</script>

<template>
  <section class="t-hero">
    <div class="t-wrap t-hero__grid" :class="{ 't-hero__grid--photo': p.image }">
      <div class="t-hero__stage">
        <SunBurst class="t-hero__sun" />
        <div class="t-hero__ring" aria-hidden="true" />
        <span class="t-spark t-spark--a" aria-hidden="true">✦</span>
        <span class="t-spark t-spark--b" aria-hidden="true">✦</span>
        <div class="t-hero__content">
          <RhText tag="h1" class="t-band" path="title" :value="p.title" ph="Título" />
          <RhText tag="p" class="t-hero__eyebrow" path="eyebrow" :value="p.eyebrow" ph="Chamada" />
          <RhText v-if="p.subtitle || editing" tag="p" class="t-hero__lead" path="subtitle" :value="p.subtitle" ph="Texto" ml />
          <div v-if="p.button || p.button2 || editing" class="t-actions t-actions--center">
            <TButton v-if="p.button || editing" class="t-btn" :link="p.link" source="abertura"><RhText path="button" :value="p.button" ph="Botão" /></TButton>
            <TButton v-if="p.button2 || editing" class="t-btn t-btn--line" :link="p.link2" source="abertura"><RhText path="button2" :value="p.button2" ph="Botão secundário" /></TButton>
          </div>
          <ul v-if="p.bullets?.length" class="t-hero__bullets">
            <li v-for="(b, i) in p.bullets" :key="i"><span aria-hidden="true">✦</span> <RhText :path="`bullets.${i}.label`" :value="b.label" ph="Destaque" /></li>
          </ul>
        </div>
      </div>
      <div v-if="p.image" class="t-hero__photo"><img :src="p.image" alt="" fetchpriority="high"></div>
    </div>
  </section>
</template>
