<script setup>
import JLiftingTab from "~/components/JLiftingTab.vue";
import JEatingTab from "~/components/JEatingTab.vue";

const liftingTab = {
  title: "Lifting",
  value: "Lifting",
  content: JLiftingTab,
};

const eatingTab = {
  title: "Eating",
  value: "Eating",
  content: JEatingTab,
};
</script>

<template>
  <header>
    <div>Gains & Grains</div>
    <button>Log out</button>
  </header>
  <JTabs :items="[liftingTab, eatingTab]"></JTabs>
  <h1>Suh dude</h1>
</template>
