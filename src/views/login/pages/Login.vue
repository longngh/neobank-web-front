<!-- eslint-disable vue/multi-word-component-names -->
<template>
  <div class="DMSans d-flex flex-column justify-center align-center login">
    <div class="sign-in-content ma-auto d-flex flex-column">
      <!-- <div class="sign-in-form ma-auto pa-12"> -->
      <div class="btn-back pa-0 cursor-pointer mr-auto mb-3">
        <router-link to="/" class="white--text text-decoration-none">
          <v-icon small color="white"> mdi-arrow-left </v-icon>
          <span class="ml-2 text-capitalize">Go Back</span>
        </router-link>
      </div>
      <v-form ref="form" lazy-validation class="sign-in-form pa-4 pa-sm-8">
        <div class="text-center font-weight-bold">
          <span :style="{ 'font-size': '30px' }"> Login</span>
        </div>
        <div class="text-xl mt-sm-4 mt-2 text-left">Email</div>
        <v-text-field
          v-model="userStore.email"
          :rules="rules.checkIdentifier"
          type="text"
          background-color="cream"
          class="mt-2"
          solo
          dense
        />
        <div class="text-xl text-left mt-sm-4">Password</div>
        <v-text-field
          v-model="userStore.password"
          :append-icon="isShowPass ? 'mdi-eye' : 'mdi-eye-off'"
          :type="isShowPass ? 'text' : 'password'"
          :rules="rules.password"
          @click:append="isShowPass = !isShowPass"
          solo
          dense
          background-color="cream"
          class="mt-2"
        />
        <div>
          <v-checkbox
            class="text-lg"
            hide-details="true"
            label="Remember me"
            v-model="userStore.rememberMe"
          />
        </div>

        <div class="text-center mt-5">
          <v-btn
            color="#5E6BE9"
            class="py-5 px-10 btn-submit white--text font-weight-bold"
            @click="submitForm"
            :disabled="!userStore.password || !userStore.email"
          >
            Let's go <v-icon class="ml-2">mdi-arrow-right</v-icon>
          </v-btn>
        </div>

        <router-link
          to="/register"
          class="text-decoration-none text-center black--text"
        >
          <div class="text-capitalize text-md cursor-pointer mt-5">
            <span :style="{ 'text-decoration': ' underline' }">
              Create New Account
            </span>
          </div>
        </router-link>
      </v-form>
    </div>
  </div>
</template>

<script>
import { mapStores } from "pinia";
import { userStore } from "@/stores/userStore";
import { rules } from "@/plugins/rules";
export default {
  components: {},
  created() {
    this.userStore.email = "";
    this.userStore.password = "";
  },
  computed: {
    ...mapStores(userStore),
  },
  data() {
    return {
      rules: rules,
      isShow: true,
      isShowPass: false,
    };
  },
  methods: {
    submitForm() {
      if (this.$refs.form.validate()) {
        this.userStore.signIn();
      }
    },
  },
};
</script>
<style lang="scss" scoped>
.login {
  width: 100%;
  height: 100vh;
  &::before {
    content: "";
    background: url("@/assets/home/intro-background.webp");
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    filter: blur(4px);
    height: 100%;
    width: 100vw;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 100;
  }
  z-index: 101;
}
.btn-back {
  z-index: 101;
}
.sign-in-content {
  width: max-content;
  height: max-content;
  z-index: 101;

  .sign-in-form {
    width: 465px;
    height: fit-content;
    font-family: Kanit, Helvetica, Arial;
    background: #ffffff;
    border-radius: 24px;
    z-index: 101;
  }
}
</style>
