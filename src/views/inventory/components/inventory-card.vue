<template>
  <v-card class="neutral30-border border-radius-16 pa-4 inventory-card" flat>
    <div class="card-image d-flex flex-column">
      <div class="full-width">
        <v-img
          class="card-image"
          height="140px"
          :src="cards.campaign.data.attributes.thumbnailUrl"
        ></v-img>
      </div>
    </div>
    <div
      class="mt-6 font-weight-bold align-center justify-center text-center text-truncate"
    >
      <div class="voucher-title">
        {{ cards.campaign.data.attributes.title }}
      </div>
    </div>
    <div
      class="d-flex font-weight-bold justify-center mt-3 column-gap-10 full-width"
    >
      <div>
        <v-img
          class="card-icon"
          :src="cards.campaignCategory.data.attributes.iconUrl"
        />
        <!-- <v-img class="card-icon" src="@/assets/redeem/card/baemin-icon.webp" /> -->
      </div>
      <v-btn
        class="border-radius-8 unpurchased px-10"
        text
        @click.stop="openClick"
      >
        <div>
          <span class="white--text font-weight-bold text-capitalize">Open</span>
        </div>
      </v-btn>
    </div>
  </v-card>
</template>

<script>
import { mapStores } from "pinia";
import { userStore } from "@/stores/userStore";
export default {
  computed: {
    ...mapStores(userStore),
  },
  props: ["cards"],
  data() {
    return {
      index: 1,
      drawer: false,
    };
  },
  methods: {
    openClick() {
      this.userStore.drawer = true;
      this.userStore.ivenCardData = this.cards;
      this.userStore.ivenVoucherQr = this.cards.qrCodeUrl;
    },
  },
};
</script>

<style lang="scss" scoped>
.card-image {
  height: 140px;
  border-radius: 8px;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  border: 1px var(--v-neutral30-base) solid;
}
.card-icon {
  border-radius: 100px;
  width: 35px;
  height: 35px;
}

.column-gap-10 {
  column-gap: 10px;
}
.tooltip {
  position: absolute;
  width: 400px;
  top: 7%;
  margin-left: 100px;
  z-index: 99;
}

.v-card {
  border-radius: 8px;
  animation: fadeleft 1s ease-in-out;
}

.unpurchased {
  width: calc(100% - 45px);
  background: var(--v-blue-base);
  padding: 4px, 16px, 4px, 16px;
}
.expired {
  width: calc(100% - 45px);
  padding: 4px, 16px, 4px, 16px;
}

.purchased {
  background: #00ff2926;
  color: #22c33c;
  padding: 4px, 16px, 4px, 16px;
}
@keyframes fadeleft {
  0% {
    opacity: 0;
    transform: translatex(-100px);
  }
  100% {
    opacity: 1;
  }
}
@keyframes fadeUp {
  from {
    opacity: 0;
    transform: translatey(300px);
  }
  to {
    opacity: 1;
  }
}
</style>
