<script setup lang="ts">
const props = defineProps<{ to: string; disabled?: boolean }>()

const isImageUrl = computed(() => /\.(png|jpg|jpeg|gif|svg)$/i.test(props.to))
const isHttp = computed(() => /^(https?:\/\/|\/\/)/.test(props.to))
const isAHref = computed(() => isHttp.value || isImageUrl.value)
</script>

<template>
  <a v-if="disabled">
    <slot />
  </a>
  <a v-else-if="isHttp" :href="props.to" target="_blank" rel="noopener noreferrer">
    <slot />
  </a>
  <router-link v-else :to="props.to">
    {{ [isHttp, isImageUrl] }}
    <slot />
  </router-link>
</template>
