<template>
  <v-menu
    offset-y
    origin="right top"
    left
    content-class="language-dropdown"
    transition="slide-y-transition"
    nudge-top="-10"
  >
    <template v-slot:activator="{ on }">
      <v-btn icon large v-on="on" class="ml-2 v-step-3">
        <img
          class="img-responsive"
          :src="`/static/flag-icons/${selectedLocale.icon}.png`"
          width="30"
        />
      </v-btn>
    </template>
    <div class="dropdown-content">
      <div class="dropdown-top d-custom-flex justify-space-between primary">
        <span class="white--text fw-bold">Languages</span>
        <!-- <span class="v-badge warning">2 NEW</span> -->
      </div>
      <v-list class="dropdown-list">
        <v-list-item
          v-for="language in languages"
          :key="language.name"
          @click="changeLanguage(language)"
        >
          <img
            class="img-responsive mr-3"
            :src="`/static/flag-icons/${language.icon}.png`"
            width="30"
          />
          <span>{{ language.name }}</span>
        </v-list-item>
      </v-list>
    </div>
  </v-menu>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  computed: {
    ...mapGetters(["selectedLocale", "languages"]),
  },
  methods: {
    changeLanguage(language) {
      this.$i18n.locale = language.locale;
      this.$store.dispatch("changeLanguage", language);
    },
  },
};
</script>