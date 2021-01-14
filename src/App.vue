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
    window.addEventListener("load", () => {
      window.scroll({
        top: 0,
        left: 0,
        behavior: "smooth",
      });
    });
  },
};
</script>

<style>
</style>
