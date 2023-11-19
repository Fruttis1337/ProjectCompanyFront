<script setup lang="ts">
import { useRouter } from 'vue-router'

const router = useRouter()

function goBack() {
  router.go(-1)
}

const { t } = useI18n()
</script>

<template>
  <nav flex="~ gap-4" mt-6 justify-center text-xl>
    <RouterLink icon-btn to="/" :title="t('button.home')">
      <div i-carbon-campsite />
    </RouterLink>

    <button icon-btn :title="t('button.back')" @click="goBack()">
      <!--  TO-DO: исправить ошибку отображения -->
      <div i="carbon-sun" />
      <!-- <Icon :icon="icons.chevronBack" /> -->
    </button>
    <button icon-btn :title="t('button.toggle_dark')" @click="toggleDark()">
      <div i="carbon-sun dark:carbon-moon" />
    </button>

    <RouterLink icon-btn to="/about" :title="t('button.about')" data-test-id="about">
      <div i-carbon-dicom-overlay />
    </RouterLink>
  </nav>
</template>
