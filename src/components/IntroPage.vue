<template>
  <section id="intro">
    <div>
      <h1>
        Pakketjes, bedrijven hebben het er maar druk mee tijdens Corona...
      </h1>
      <HandlerSvg name="arrow" />
      <HandlerSvg name="webcam" />
    </div>
    <div class="video-container">
      <video id="animation1">
        <source src="../../public/assets/animatie1.mp4" type="video/mp4" />
      </video>
    </div>
  </section>
</template>

<script>
import HandlerSvg from "./HandlerSvg.vue";
export default {
  name: "IntroPage",
  components: {
    HandlerSvg,
  },
  mounted() {
    const firstAnimation = document.getElementById("animation1");
    const x = window.matchMedia("(max-width: 1440px)");
    const body = document.querySelector("body");

    if (firstAnimation) {
      window.addEventListener("keydown", (event) => {
        const key = event.which || event.keyCode;

        if (key === 32) {
          event.preventDefault();

          firstAnimation.paused
            ? firstAnimation.play()
            : firstAnimation.pause();
        }
      });
    }

    firstAnimation.addEventListener("ended", () => {
      if (x.matches) {
        window.scrollBy(0, 1050);
      } else {
        window.scrollBy(0, 1300);
      }

      body.style.overflowY = "visible";
    });
  },
  methods: {},
};
</script>

<style>
#intro {
  height: 100vh;
  overflow: hidden;
  transition: 0.5s opacity;
}
#intro h1 {
  font-family: "Mont Heavy";
  font-size: 4em;
  max-width: 55%;
  transform: translateY(80%);
  transition: all 1.5s;
  position: relative;
  left: 100px;
}

.video-container {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  opacity: 0;
  z-index: -1;
}
.video-container video {
  min-width: 100%;
  min-height: 100%;
  width: 100% !important;
  height: auto !important;
  position: absolute;
  top: 55%;
  left: 50%;
  object-fit: cover;
  transform: translate(-50%, -50%);
}

@media only screen and (max-width: 1440px) {
  #intro h1 {
    font-size: 3.5em;
    transform: translateY(55%);
    left: 70px;
  }

  .video-container video {
    top: 52.5%;
  }
}
</style>