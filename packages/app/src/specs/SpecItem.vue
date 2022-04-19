<template>
  <div
    class="h-full grid gap-8px grid-cols-[16px,auto,auto] items-center"
    data-cy="spec-item"
  >
    <i-cy-document-plus_x16
      v-if="gitInfo?.statusType === 'created'"
      class="icon-light-jade-50 icon-dark-jade-400"
    />
    <i-cy-document-plus-minus_x16
      v-else-if="gitInfo?.statusType === 'modified'"
      class="icon-light-orange-50 icon-dark-orange-400"
    />
    <i-cy-document-blank_x16
      v-else
      class="icon-light-gray-50 icon-dark-gray-400"
    />

    <div class="text-gray-400 text-indigo-500 group-hocus:text-indigo-600">
      <HighlightedText
        :text="fileName"
        :indexes="indexes.filter((idx) => idx < fileName.length)"
        class="font-medium text-indigo-500 group-hocus:text-indigo-600"
        highlight-classes="text-gray-1000"
      />
      <HighlightedText
        :text="extension"
        :indexes="indexes.filter((idx) => idx >= fileName.length).map(idx => idx - fileName.length)"
        class="font-light group-hocus:text-gray-400"
        highlight-classes="text-gray-1000"
      />
    </div>
  </div>
</template>

<script lang="ts" setup>
import type { SpecListRowFragment } from '../generated/graphql'
import HighlightedText from './HighlightedText.vue'

withDefaults(defineProps<{
  fileName: string
  extension: string
  indexes?: number[]
  gitInfo: SpecListRowFragment
}>(), { indexes: () => [] })
</script>
