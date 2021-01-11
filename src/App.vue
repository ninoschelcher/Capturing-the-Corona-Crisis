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
  created() {
    window.scrollTo(0, 0);
  },
};
</script>

<style>
</style>
