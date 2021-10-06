<template>
  <input
    type="checkbox"
    class="m-0"
    :checked="modelValue"
    @change="e => { $emit('update:modelValue', (e.target as HTMLInputElement).checked) }"
  >
</template>

<script setup lang="ts">
import { defineEmits, defineProps } from 'vue'

defineProps<{
    modelValue: boolean
}>()

defineEmits<{(e: 'update:modelValue', value: boolean): void
}>()
</script>
