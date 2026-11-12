<script setup lang="ts">
const props = defineProps<{ section: { id: string, props: Record<string, any> } }>()
const p = computed(() => props.section.props)
const store = useRhStore()
const company = useRhCompany()
const { global, menu } = useRhSite()
const header = computed(() => global('header')?.props ?? {})
const name = computed(() => company.text(header.value.logo) || store.value?.name || '')
const crest = computed(() => header.value.logoImage || store.value?.logoUrl || '')
const insta = computed(() => company.values.value.instagram)
</script>

<template>
  <footer class="t-footer">
    <div class="t-rule" />
    <div class="t-wrap t-footer__grid">
      <div>
        <p class="t-footer__name">{{ name }}</p>
        <RhText tag="p" class="t-footer__about" path="about" :value="p.about" ph="Sobre a marca" ml />
      </div>
      <div class="t-footer__crest">
        <span><img v-if="crest" :src="crest" :alt="name"><SunBurst v-else :rays="24" /></span>
      </div>
      <div class="t-footer__contact">
        <div class="t-footer__social">
          <a v-if="insta" :href="`https://www.instagram.com/${insta.replace('@', '')}/`" target="_blank" rel="noopener" aria-label="Instagram">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"><rect x="3" y="3" width="18" height="18" rx="5" /><circle cx="12" cy="12" r="4" /><circle cx="17.5" cy="6.5" r="1" fill="currentColor" stroke="none" /></svg>
          </a>
          <RhWhatsappButton source="rodape" aria-label="WhatsApp">
            <svg viewBox="0 0 24 24" fill="currentColor"><path d="M12 2a10 10 0 0 0-8.6 15.1L2 22l5-1.3A10 10 0 1 0 12 2Zm4.5 12.1c-.2-.1-1.5-.7-1.7-.8-.2-.1-.4-.1-.6.1l-.8 1c-.1.2-.3.2-.5.1a6.7 6.7 0 0 1-3.3-2.9c-.2-.4.2-.4.7-1.3.1-.2 0-.3 0-.4l-.8-1.8c-.2-.5-.4-.4-.6-.4h-.5a1 1 0 0 0-.7.3 3 3 0 0 0-.9 2.2 5.2 5.2 0 0 0 1.1 2.7 11.8 11.8 0 0 0 4.5 4c1.7.7 2.3.8 3.2.6a2.7 2.7 0 0 0 1.7-1.2 2.2 2.2 0 0 0 .2-1.2c-.1-.1-.3-.2-.5-.3Z" /></svg>
          </RhWhatsappButton>
        </div>
        <RhText tag="p" path="whatsapp" :value="p.whatsapp" ph="WhatsApp" />
        <RhText tag="p" path="email" :value="p.email" ph="E-mail" />
        <RhText tag="p" path="hours" :value="p.hours" ph="Horário" />
      </div>
    </div>
    <div class="t-wrap t-footer__copy">
      <nav aria-label="Rodapé">
        <NuxtLink to="/">Início</NuxtLink>
        <NuxtLink to="/loja">{{ company.text(header.shopLabel) || 'Loja' }}</NuxtLink>
        <NuxtLink v-for="m in menu" :key="m.id" :to="m.slug">{{ m.title }}</NuxtLink>
        <NuxtLink to="/minha-conta">Minha conta</NuxtLink>
      </nav>
      <p>© {{ new Date().getFullYear() }} {{ name }} · <RhText path="note" :value="p.note" ph="Linha final" /></p>
    </div>
  </footer>
</template>
