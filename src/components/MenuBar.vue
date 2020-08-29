<template>
  <v-app-bar app color="primary" dark>
    <!-- <div class="d-flex align-center">
      <v-img
        alt="Vuetify Logo"
        class="shrink mr-2"
        contain
        src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
        transition="scale-transition"
        width="40"
      />

      <v-img
        alt="Vuetify Name"
        class="shrink mt-1 hidden-sm-and-down"
        contain
        min-width="100"
        src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
        width="100"
      />
    </div> -->

    <v-spacer></v-spacer>

    <v-btn @click="logout">
      <span class="mr-2">Logout</span>
      <v-icon>mdi-home-export-outline</v-icon>
    </v-btn>
  </v-app-bar>
</template>

<script>
// @ is an alias to /src

export default {
  name: "MenuBar",
  components: {},
  methods: {
    logout() {
      // ログアウト処理実施
      this.$store.dispatch('logout');
    },
  },
};
</script>