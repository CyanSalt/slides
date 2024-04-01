<script lang="ts" setup>
import { ArrowRight } from 'lucide'
import { RIcon } from 'roughness'
</script>

<template>
  <div class="pt-12">
    <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer inline-flex gap-2 items-center" hover="bg-white bg-opacity-10">
      <slot>开始</slot> <RIcon :icon="ArrowRight" />
    </span>
  </div>
</template>
