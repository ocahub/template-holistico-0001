<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const { editing } = useRhSite()
</script>

<template>
  <section class="t-quoteband">
    <SunBurst class="t-quoteband__sun" :rays="36" />
    <div class="t-wrap t-center">
      <span class="t-quoteband__arrow" aria-hidden="true">
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M12 5v14m0 0 6-6m-6 6-6-6" /></svg>
      </span>
      <RhText tag="blockquote" class="t-quote" path="text" :value="p.text" ph="Frase" ml />
      <TButton v-if="p.button || editing" class="t-btn" :link="p.link" source="citacao"><RhText path="button" :value="p.button" ph="Botão" /></TButton>
    </div>
  </section>
</template>
