<script setup>
definePageMeta({
  middleware: () => {
    if (!useRuntimeConfig().public.pwaEnabled)
      return navigateTo('/')
  },
})

useWebShareTarget()

const pwaIsInstalled = process.server ? false : useNuxtApp().$pwa.isInstalled
</script>

<template>
  <MainContent>
    <template #title>
      <NuxtLink to="/share-target" flex items-center gap-2>
        <div i-ri:share-line />
        <span>{{ $t('share-target.title') }}</span>
      </NuxtLink>
    </template>
    <slot>
      <div flex="~ col" px5 py2 gap-y-4>
        <div
          v-if="!pwaIsInstalled || !currentUser"
          role="alert"
          gap-1
          p-2
          text-red-600 dark:text-red-400
          border="~ base rounded red-600 dark:red-400"
        >
          {{ $t('share-target.hint') }}
        </div>
        <div>{{ $t('share-target.description') }}</div>
      </div>
    </slot>
  </MainContent>
</template>
