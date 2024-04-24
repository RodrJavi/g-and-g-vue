<script setup>
import JLiftingTab from "~/components/JLiftingTab.vue";
import JEatingTab from "~/components/JEatingTab.vue";

const props = defineProps({
  items: Array,
});

const currentTab = ref("");

const updateCurrentTab = (value) => {
  currentTab.value = value;
};
</script>

<template>
  <div>
    <div>
      <label v-for="tab in props.items" :key="tab">
        <input
          type="radio"
          v-model="currentTab"
          :checked="tab === currentTab"
          @change="updateCurrentTab(tab)" />
        {{ tab }}
      </label>
    </div>
    <div v-if="currentTab == ''">Pick a tab to start!</div>
    <div v-else>
      {{ currentTab }}
    </div>
  </div>
</template>
