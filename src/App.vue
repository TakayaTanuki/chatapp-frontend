<template>
  <v-app>
    <login v-if="!isLogin"></login>
    <home v-else />
  </v-app>
</template>

<script>
import Login from "@/views/Login.vue";
import Home from "@/views/Home.vue";
import { mapState } from "vuex";

export default {
  name: "App",
  components: {
    Login,
    Home,
  },
  // data: () => ({
  //   isLogin: false,
  // }),
  computed: {
    /* 
    スプレッド演算子を使うことで以下と同じコードになる。
    mapState({
      isLogin: this.$store.state.isLogin,
    })
    */
    ...mapState(["isLogin"]),
  },
  // mounted() {
  //   this.$store.watch(
  //     (state) => (state.userId, state.password),
  //     (userId, password) => {
  //       console.log(
  //         `変更が検知されました。userId:${userId}/password:${password}`
  //       );
  //       this.isLogin = true;
  //     }
  //   );
  // },
};
</script>
