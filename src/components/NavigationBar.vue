<template>
  <div class="d-flex nav-bar">
    <div
      v-if="homeStore.scrollY < 1100 && homeStore.scrollY > 90"
      class="d-flex gap-24 DMSans nav-container justify-center align-center mx-auto pa-7"
    >
      <v-img
        class="nav-logo align-self-center"
        :src="require(`@/assets/home/web-logo.webp`)"
      />
      <router-link
        to="/home"
        class="text-decoration-none align-self-center"
        active-class="active"
      >
        <div class="text-none text-uppercase nav-link">HOME</div>
      </router-link>
      <router-link
        to="/world"
        class="text-decoration-none align-self-center"
        active-class="active"
      >
        <div class="text-none text-uppercase nav-link">WORLD</div>
      </router-link>
      <router-link
        to="/redeem"
        class="text-decoration-none align-self-center"
        active-class="active"
      >
        <div class="text-none text-uppercase nav-link">REDEEM</div>
      </router-link>
      <router-link
        v-if="!userStore.isConnected"
        to="/login"
        class="text-decoration-none align-self-center"
        active-class="active"
      >
        <div class="text-none text-uppercase nav-link">LOGIN</div>
      </router-link>
    </div>

    <div
      v-else-if="homeStore.scrollY > 90"
      class="d-flex gap-24 DMSans nav-container-white justify-center align-center mx-auto pa-7"
    >
      <v-img
        class="nav-logo align-self-center"
        :src="require(`@/assets/home/web-logo.webp`)"
      />
      <router-link
        to="/home"
        class="text-decoration-none align-self-center"
        active-class="active"
      >
        <div class="text-none text-uppercase nav-link">HOME</div>
      </router-link>
      <router-link
        to="/world"
        class="text-decoration-none align-self-center"
        active-class="active"
      >
        <div class="text-none text-uppercase nav-link">WORLD</div>
      </router-link>
      <router-link
        to="/redeem"
        class="text-decoration-none align-self-center"
        active-class="active"
      >
        <div class="text-none text-uppercase nav-link">REWARD</div>
      </router-link>
      <router-link
        to="/login"
        class="text-decoration-none align-self-center"
        active-class="active"
      >
        <div class="text-none text-uppercase nav-link">LOGIN</div>
      </router-link>
    </div>
  </div>
</template>

<script>
import { mapStores } from "pinia";
import { userStore } from "../stores/userStore";
import { homeStore } from "@/views/home/store/homeStore";
export default {
  data() {
    return {};
  },
  computed: {
    ...mapStores(userStore),
    ...mapStores(homeStore),
  },
};
</script>

<style lang="scss" scoped>
a {
  color: black !important;
}
.active {
  color: var(--v-primary-base) !important;
}
.nav-bar {
  width: 100%;
  position: fixed;
  z-index: 99;
  margin-top: 40px;
}
.nav-container {
  border-radius: 40px;
  background: rgba(255, 249, 247, 0.2);
  color: white;
  height: 60px;
  font-size: 16px;
  font-weight: bold;
  width: max-content;
}

.nav-container-white {
  border: 5px black solid;
  border-radius: 40px;
  background: white;
  color: white;
  height: 60px;
  font-size: 16px;
  font-weight: bold;
  width: max-content;
}
.nav-logo {
  height: 38px;
  width: 158px;
}
.gap-24 {
  gap: 24px;
}
.active:hover {
  color: #2970ff;
}
</style>
