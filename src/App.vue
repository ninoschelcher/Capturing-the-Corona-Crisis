<template>
  <LineChart />
  <CircularChart />
  <Intro />
  <SorteerCentrum />
  <DozenStapel />
  <BestelBusje />
</template>

<script>
import DozenStapel from "./components/DozenStapel.vue";
import CircularChart from "./components/CircularChart.vue";
import LineChart from "./components/LineChart.vue";

export default {
  name: "App",
  components: {
    DozenStapel,
    CircularChart,
    LineChart,
  },
};
</script>

<style>
</style>
