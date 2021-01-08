<template>
  <IntroPage />
  <CircularChart />
  <LineChart />
  <DozenStapel />
</template>

<script>
import IntroPage from "./components/IntroPage.vue";
import DozenStapel from "./components/DozenStapel.vue";
import LineChart from "./components/LineChart.vue";

export default {
  name: "App",
  components: {
    IntroPage,
    DozenStapel,
    LineChart,
  },
};
</script>

<style>
</style>
