<template>
  <v-card flat class="form-detail mt-4 full-width pa-6">
    <v-form @submit.prevent="editAccount" id="check-edit-form" ref="form">
      <div class="user-image" v-if="!userStore.userData.avatarUrl">
        <v-img
          :style="{ 'border-radius': '100px' }"
          :src="require(`@/assets/profile-pic.webp`)"
        />
      </div>
      <div class="user-image" v-else>
        <v-img
          :style="{ 'border-radius': '100px' }"
          :src="userStore.userData.avatarUrl"
        />
      </div>

      <v-row no-gutters>
        <v-col cols="3"
          ><div class="text-left text-md font-weight-700 mt-2">Avatar</div>
        </v-col>
        <v-col cols="4">
          <v-file-input
            v-if="!profileEdit"
            class="pa-0"
            height="36px"
            disabled
            prepend-icon=""
            prepend-inner-icon="mdi-upload"
            background-color="neutral10"
            solo
            dense
            flat
          >
          </v-file-input>
          <v-file-input
            v-else
            v-model="userStore.file"
            accept="image/png, image/jpeg, image/bmp,image/webp"
            ref="myfile"
            class="pa-0"
            height="36px"
            @change="onFileChanged($event)"
            prepend-icon=""
            prepend-inner-icon="mdi-upload"
            dense
            flat
            outlined
          ></v-file-input>
        </v-col>
      </v-row>
      <v-row no-gutters>
        <v-col cols="3"
          ><div class="text-left text-md font-weight-700 mt-2">First name</div>
        </v-col>
        <v-col cols="4">
          <v-text-field
            v-if="!profileEdit"
            v-model="userStore.userData.userMetadata.firstName"
            height="36px"
            type="text"
            class="pa-0"
            placeholder=""
            background-color="neutral10"
            solo
            readonly
            dense
            flat
          />
          <v-text-field
            v-else
            v-model="userStore.userData.userMetadata.firstName"
            height="36px"
            type="text"
            class="pa-0"
            placeholder=""
            outlined
            dense
            flat
          />
        </v-col>
      </v-row>
      <v-row no-gutters>
        <v-col cols="3"
          ><div class="text-left text-md font-weight-700 mt-2">Last name</div>
        </v-col>
        <v-col cols="4">
          <v-text-field
            v-if="!profileEdit"
            v-model="userStore.userData.userMetadata.lastName"
            height="36px"
            type="text"
            class="pa-0"
            placeholder=""
            background-color="neutral10"
            solo
            readonly
            dense
            flat
          />
          <v-text-field
            v-else
            v-model="userStore.userData.userMetadata.lastName"
            height="36px"
            type="text"
            class="pa-0"
            placeholder=""
            outlined
            dense
            flat
          />
        </v-col>
      </v-row>
      <v-row no-gutters>
        <v-col cols="3"
          ><div class="text-left text-md font-weight-700 mt-2">Email</div>
        </v-col>
        <v-col cols="4">
          <v-text-field
            v-if="!profileEdit"
            v-model="userStore.userData.email"
            height="36px"
            type="text"
            class="pa-0"
            placeholder=""
            background-color="neutral10"
            solo
            readonly
            dense
            flat
          />
          <v-text-field
            v-else
            v-model="userStore.userData.email"
            height="36px"
            type="text"
            class="pa-0"
            placeholder=""
            outlined
            dense
            flat
          />
        </v-col>
      </v-row>
      <v-row no-gutters>
        <v-col cols="3"
          ><div class="text-left text-md font-weight-700 mt-2">Telephone</div>
        </v-col>
        <v-col cols="4">
          <v-text-field
            v-if="!profileEdit"
            v-model="userStore.userData.userMetadata.phoneNumber"
            height="36px"
            type="text"
            class="pa-0"
            placeholder=""
            background-color="neutral10"
            solo
            readonly
            dense
            flat
          />
          <v-text-field
            v-else
            v-model="userStore.userData.userMetadata.phoneNumber"
            height="36px"
            type="text"
            :rules="rules.phone"
            class="pa-0"
            placeholder=""
            outlined
            dense
            flat
          />
        </v-col>
      </v-row>

      <v-divider class="mb-6" />
      <div class="d-flex gap-8">
        <v-btn
          class="text-capitalize text-btn"
          variant="text"
          @click="profileEdit = true"
          v-if="!profileEdit"
          outlined
          depressed
        >
          Edit
        </v-btn>
        <div class="d-flex gap-8" v-else>
          <v-btn
            class="text-capitalize"
            variant="text"
            @click="profileEdit = false"
            outlined
            depressed
          >
            Cancel
          </v-btn>

          <v-btn
            class="text-capitalize"
            type="submit"
            form="check-edit-form"
            color="primary"
            :disabled="
              !userStore.file ||
              !userStore.userData.userMetadata.firstName ||
              !userStore.userData.userMetadata.lastName ||
              !userStore.userData.email ||
              !userStore.userData.userMetadata.phoneNumber
            "
            depressed
          >
            Save
          </v-btn>
        </div>
      </div>
    </v-form>
  </v-card>
</template>

<script>
import { mapStores } from "pinia";
import { userStore } from "@/stores/userStore";
import { rules } from "@/plugins/rules";

export default {
  computed: {
    ...mapStores(userStore),
  },
  data() {
    return {
      rules: rules,
      profileEdit: false,
    };
  },
  methods: {
    onFileChanged(data) {
      this.userStore.file = data;
      console.log("file", data);
    },

    editAccount() {
      this.userStore.updateAccountSetting();
      this.profileEdit = false;

    },
  },
};
</script>

<style lang="scss" scoped>
@keyframes fadeleft {
  0% {
    opacity: 0;
    transform: translatex(-100px);
  }
  100% {
    opacity: 1;
  }
}
.form-detail {
  background-color: white;
  height: max-content !important;
  border: 1px solid #e3e8ef;
}

.v-card {
  border-radius: 12px !important;
}
.user-logo {
  height: 39px;
  width: 100px;
}
.user-image {
  height: 79px;
  width: 64px;
}
.btn-customize {
  width: 300px;
  background: white;
  border-radius: 8px;
  border: 1px solid #e3e8ef;
}
</style>
