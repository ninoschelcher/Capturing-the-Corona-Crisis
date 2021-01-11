<template>
  <IntroPage />
  <DozenStapel />
</template>

<script>
import IntroPage from "./components/IntroPage.vue";
import DozenStapel from "./components/DozenStapel.vue";

export default {
  name: "App",
  components: {
    IntroPage,
    DozenStapel,
  },
};
</script>

<style>
</style>
