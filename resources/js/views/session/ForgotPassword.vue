<template>
  <div class="session-wrapper">
    <div class="session-left">
      <session-slider-widget></session-slider-widget>
    </div>
    <div class="session-right text-center">
      <div class="session-table-cell">
        <div class="session-content">
          <img
            :src="appLogoF"
            class="img-responsive mb-4"
            style="width: 70%; height: auto"
          />
          <h2 class="mb-4">{{ $t("message.forgotPassword") }}</h2>
          <p class="fs-14">
            {{ $t("message.enterYourEmailToSendYouAResetLink") }}.
          </p>
          <v-form v-model="valid" class="mb-6">
            <v-text-field
              label="E-mail ID"
              v-model="email"
              :rules="emailRules"
              required
            ></v-text-field>
            <v-btn color="primary" block to="/session/reset-password"
              >Send Email</v-btn
            >
          </v-form>
          <div>
            <router-link to="/session/login">{{
              $t("message.backToSignIn")
            }}</router-link>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script>
import SessionSliderWidget from "Components/Widgets/SessionSlider";
import { mapGetters } from "vuex";

export default {
  components: {
    SessionSliderWidget,
  },
  computed: {
    ...mapGetters(["appLogo", "darkLogo"]),
    ...{
      appLogoF() {
        // if (this.$vuetify.theme.dark)
        return this.appLogo;
        // return this.darkLogo;
      },
    },
  },
  data() {
    return {
      email: "",
      valid: false,
      emailRules: [
        (v) => !!v || "E-mail is required",
        (v) =>
          /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) ||
          "E-mail must be valid",
      ],
    };
  },
};
</script>