
<script setup>
import GoogleLogin from "~/components/GoogleLogin.vue";

definePageMeta({
  title: 'pages.title.top' // set resource key
})

const { locale, locales, t } = useI18n()
const switchLocalePath = useSwitchLocalePath()

const availableLocales = computed(() => {
  return (locales.value).filter(i => i.code !== locale.value)
})
</script>

<template>
  <div>
    <p>{{ t('pages.title.top') }}</p>
    <p>{{ t('pages.title.about') }}</p>
    <nav>
      <template v-for="(locale, index) in availableLocales" :key="locale.code">
        <template v-if="index"> | </template>
        <NuxtLink :to="switchLocalePath(locale.code)">{{ locale.name ?? locale.code }}</NuxtLink>
      </template>
    </nav>
    <LandSwitcher />
<!--    <GoogleSignInButton />-->
    <GoogleLogin />
  </div>
</template>
