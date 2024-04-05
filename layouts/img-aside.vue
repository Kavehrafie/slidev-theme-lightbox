<script setup lang="ts">
import { ref } from 'vue'


const props = defineProps({
  imageSrc: {
    type: String,
    required: true
  },
  caption: {
    type: String,
  },
  class: {
    type: String,
  },
  layoutClass: {
    type: String,
  },
  CDN: {
    type: String,
    default: "https://d38ruy7cl1ctq5.cloudfront.net"
  },
  operations: {
    type: Object,
    default: () => ({
      format: 'auto'
    })
  }
})

const operationsToStrings = ref<string[]>([])

for (const [key, value] of Object.entries(props?.operations)) {
  operationsToStrings.value.push(`${key}=${value}`)
}

</script>

<template>
  <div class="slidev-layout two-columns w-full h-full flex gap-4 items-end" :class="props.layoutClass">
    <div class="flex gap-2 flex-col">
      <slot name="aside" />
      <img
        :src="`${props.CDN}/${props?.imageSrc}${operationsToStrings.length > 0 ? '?' + operationsToStrings.join('&') : ''}`"
        class="w-full h-full object-cover" />
    </div>
    <div class="flex flex-col gap-2 justify-between h-full" :class="props.class">
      <div>
        <slot />
      </div>

      <span class="text-sm pb-0" v-if="props.caption">{{ props.caption }}</span>
    </div>
  </div>
</template>
