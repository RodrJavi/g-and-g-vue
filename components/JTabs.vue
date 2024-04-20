<script setup>
const props = defineProps({
  items: Array,
});

const currentTab = ref(props.items[0].value);
const currentItem = props.items.find((tab) => tab.value === currentTab.value);
const updateCurrentTab = (value) => {
  currentTab.value = value;
};
</script>

<template>
  <div>
    <div>
      <label v-for="tab in props.items" :key="tab.value">
        <input
          type="radio"
          v-model="currentTab"
          :checked="tab.value === currentTab"
          @change="updateCurrentTab(tab.value)" />
        {{ tab.title }}
      </label>
    </div>
    <component :is="currentItem.content"></component>
    {{ currentTab }}
  </div>
</template>
