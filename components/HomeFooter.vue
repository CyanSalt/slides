<script lang="ts" setup>
import { Github, PencilLine } from 'lucide'
import { RIcon } from 'roughness'
</script>

<template>
  <div class="abs-br m-6 flex gap-2">
    <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 inline-flex !border-none !hover:text-white">
      <RIcon :icon="PencilLine" />
    </button>
    <a href="https://github.com/CyanSalt/slides" target="_blank" alt="GitHub" title="Open in GitHub"
      class="text-xl slidev-icon-btn opacity-50 inline-flex !border-none !hover:text-white">
      <RIcon :icon="Github" />
    </a>
  </div>
</template>
