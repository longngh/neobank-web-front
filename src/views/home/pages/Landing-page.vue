<template>
  <div class="home mx-auto">
    <div
      v-if="windowWidth > 1280 || homeStore.scrollY < 1070"
      class="doorway tag"
      :style="{
        backgroundImage: 'url(' + require(`@/assets/home/door.webp`) + ')',
      }"
    />

    <div
      v-if="windowWidth > 1280 || homeStore.scrollY < 1070"
      class="introduction-content d-flex flex-column justify-center align-center row-gap-30 full-width"
    >
      <div
        class="text-center white--text text-dp-xxl font-weight-700"
        :style="{ width: '500px' }"
      >
        Welcome to VParadise
      </div>
      <div
        class="text-center white--text text-dp-xs"
        :style="{ width: '700px' }"
      >
        Journey into the future of banking with VParadise, a harmony between
        technologies and banking
      </div>
      <v-btn
        color="lightblue"
        class="white--text pa-5"
        href="https://dev-neobank-game-vietin.capylabs.io/"
      >
        <div class="text-decoration-none text-sm">Discover now</div>
        <v-icon color="white"> mdi-arrow-right-thin </v-icon>
      </v-btn>
    </div>

    <introduction />
    <v-img class="redblur-image" :src="require(`@/assets/red-blur.webp`)">
    </v-img>
    <v-img class="blueblur-image" :src="require(`@/assets/blue-blur.webp`)">
    </v-img>
    <div class="container DMSans mx-auto d-flex flex-column">
      <firstsection />

      <secondSection />
      <thirdSection />
    </div>
    <FooterLanding />
  </div>
</template>

<script>
import FooterLanding from "@/views/home/components/landing/landing-footer.vue";
import firstSectionVue from "../components/landing/landing-first-section.vue";
import introductionVue from "../components/landing/landing-introduction.vue";
import secondsection from "../components/landing/landing-second-section.vue";
import thirdSectionVue from "../components/landing/landing-third-section.vue";
import { mapStores } from "pinia";
import { homeStore } from "@/views/home/store/homeStore";

export default {
  name: "HomeView",
  components: {
    introduction: introductionVue,
    firstsection: firstSectionVue,
    secondSection: secondsection,
    thirdSection: thirdSectionVue,
    FooterLanding: FooterLanding,
  },
  computed: {
    ...mapStores(homeStore),
  },
  data() {
    return {
      index: 1,
      scrollValue: 0,
      windowWidth: window.innerWidth,
    };
  },
  created() {
    window.addEventListener("scroll", this.handleScroll);
  },
  // eslint-disable-next-line vue/no-deprecated-destroyed-lifecycle
  beforeDestroy() {
    window.removeEventListener("scroll", this.handleScroll);
  },
  methods: {
    handleScroll() {
      const doorway = document.querySelector(".doorway");
      const introduction = document.querySelector(".introduction");
      const content = document.querySelector(".introduction-content");
      const container = document.querySelector(".container");
      const scrollY = window.scrollY;
      this.scrollValue = scrollY;
      this.homeStore.scrollY = scrollY;
      console.log(scrollY);

      if (this.homeStore.scrollY >= 1105) {
        introduction.style.position = "relative";
        content.style.position = "absolute";
        content.style.zIndex = "0";
        doorway.style.zIndex = "1";
        doorway.style.display = "none";
        container.style.opacity = "1";
        introduction.style.animation = " zoom-in-zoom-out 0.1s ease-out";
        content.style.animation = " zoom-in-zoom-out 0.1s ease-out";
        container.style.animation = " zoom-out-zoom-in 2s ease-out";
      } else {
        introduction.style.position = "fixed";
        content.style.position = "fixed";
        content.style.zIndex = "4";
        doorway.style.display = "block";
        container.style.opacity = "0.1";
        container.style.animation = " zoom-in-zoom-out 0.1s ease-out";
        introduction.style.animation = " zoom-out-zoom-in 2s ease-out";
        content.style.animation = " zoom-out-zoom-in 2s ease-out";
        doorway.style.zIndex = "4";
      }
      doorway.style.backgroundSize = 100 + scrollY / 7 + "%";
      doorway.style.opacity = 1 + scrollY / 6 + "";
    },
  },
};
</script>

<style lang="scss">
.home {
  overflow-x: hidden !important;
  background-color: #0c0e12;
}
.doorway {
  position: fixed;
  height: 100vh;
  width: 100%;
  top: 0;
  left: 0;
  z-index: 4;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}
.introduction-content {
  position: fixed;
  height: 100vh;
  z-index: 4;
}
.container {
  @media (min-width: 1920px) {
    width: 1560px;
  }

  overflow-x: hidden !important;
  overflow-y: hidden !important;
  row-gap: 150px;
  z-index: 2;
  padding-top: 400px;
  padding-bottom: 100px;
}

.tag {
  opacity: 1;
}
.tag.visible {
  opacity: 0;
  transition: all 1s;
}
@media (max-width: 1280px) {
  .rectangle {
    display: none !important;
  }
}
.content-title {
  text-align: left;
  @media (max-width: 1280px) {
    text-align: center !important;
  }
}
.logo-group {
  @media (max-width: 1280px) {
    margin: 0 auto;
  }
}
@keyframes zoom-out-zoom-in {
  0% {
    transform: scale(1, 1);
    opacity: 0;
  }
  50% {
    transform: scale(1.1, 1.1);
    opacity: 0.5;
  }
  100% {
    transform: scale(1, 1);
    opacity: 1;
  }
}
@keyframes zoom-in-zoom-out {
  0% {
    transform: scale(1.15, 1.15);
    opacity: 1;
  }
  50% {
    transform: scale(1.1, 1.1);
    opacity: 0.5;
  }
  100% {
    transform: scale(1, 1);
    opacity: 0;
  }
}
.redblur-image {
  z-index: 2;
  position: absolute;
  width: 1000px;
  height: 400px;
  filter: blur(60px);
  transform: matrix(-1, 0, 0, 1, 0, 0);
  opacity: 0.5;
  bottom: 5%;
  left: -9%;
}
.blueblur-image {
  z-index: 2;
  position: absolute;
  width: 300px;
  height: 200vh;
  filter: blur(80px);
  opacity: 0.5;
  transform: matrix(-1, 0, 0, 1, 0, 0);
  top: 30%;
  right: -5%;
}
.row-gap-30 {
  row-gap: 30px;
}
</style>
