<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
</script>

<template>
  <section class="t-cta">
    <SunBurst class="t-cta__sun" />
    <div class="t-wrap t-center">
      <span class="t-spark-row" aria-hidden="true">✦ ✦ ✦</span>
      <RhText tag="h2" class="t-cta__title" path="title" :value="p.title" ph="Título" />
      <RhText tag="p" class="t-cta__text" path="text" :value="p.text" ph="Texto" ml />
      <div class="t-actions t-actions--center">
        <TButton class="t-btn" :link="p.link" source="chamada"><RhText path="button" :value="p.button" ph="Botão" /></TButton>
        <RhWhatsappButton v-if="p.whatsapp || editing" class="t-btn t-btn--ghost" source="chamada"><RhText path="whatsapp" :value="p.whatsapp" ph="Botão do WhatsApp" /></RhWhatsappButton>
      </div>
    </div>
  </section>
</template>
