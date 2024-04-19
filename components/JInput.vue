<script lang="ts" setup>
const props = defineProps<{
  type: string;
  label: string;
  placeholder?: string;
}>();

const modelValue = defineModel({ default: "" });
</script>

<template>
  <label class="flex flex-col">
    <span class="block">{{ label }}</span>
    <input
      class="border border-gray-300 rounded-md px-2 py-1"
      :type="props.type"
      :placeholder="props.placeholder"
      v-model="modelValue" />
  </label>
</template>
