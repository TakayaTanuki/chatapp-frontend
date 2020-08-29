<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12" style="height:80vh">
        <v-toolbar color="#BBDEFB" light>
          <v-toolbar-title>Welcome ChatApp</v-toolbar-title>
          <v-spacer></v-spacer>
          <!-- <v-btn @click="deleteRecord">
            <v-icon>mdi-magnify</v-icon>Delete Old Chat
          </v-btn> -->
        </v-toolbar>
        <!-- v-card内チャットをスクロールさせるためにclass="overflow-y-auto"を指定 -->
        <v-card height="90%" width="100%" class="overflow-y-auto">
          <!-- チャットの表示 -->
          <v-list two-line subheader>
            <v-list-item v-for="(message,index) in messages" :key="index">
              <v-list-item-avatar>
                <v-icon>mdi-account-circle</v-icon>
              </v-list-item-avatar>
              <v-list-item-content>
                <v-list-item-title v-text="message.id"></v-list-item-title>
                <v-list-item-subtitle v-text="message.message"></v-list-item-subtitle>
                <v-list-item-subtitle v-text="message.time"></v-list-item-subtitle>
              </v-list-item-content>
            </v-list-item>
            <v-divider inset v-if="messages.length > 0"></v-divider>
          </v-list>
        </v-card>
        <v-card height="10%" width="100%" color="#B2DFDB" class="pa-sm-3 pa-lg-3 pa-md-4">
          <v-text-field
            v-model="message"
            solo
            clearable
            append-outer-icon="mdi-send"
            @click:append-outer="sendMessage"
            @keyup.enter="sendMessage"
          ></v-text-field>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import io from "socket.io-client";
// import axios from "axios";

export default {
  name: "Chat",
  data: () => ({
    message: "",
    messages: [],
    socket: "",
    userId: "",
  }),
  methods: {
    //チャットを投稿する処理

    // ToDo Indexの調整
    sendMessage() {
      this.userId = this.$store.state.userId;
      console.log(this.$store.state.userId);
      console.log(this.userId);
      const date = new Date();
      const time = `${date.getFullYear().toString()}-${(
        "00" + (date.getMonth() + 1).toString()
      ).slice(-2)}-${("00" + date.getDate().toString()).slice(-2)} ${(
        "00" + date.getHours().toString()
      ).slice(-2)}:${("00" + date.getMinutes().toString()).slice(-2)}:${(
        "00" + date.getSeconds().toString()
      ).slice(-2)}`;
      this.socket.emit("SEND_MESSAGE", {
        // index: this.messages.length + 1,
        id: this.userId,
        message: this.message,
        time: time,
      });
      this.message = "";
    },
    // ToDo 削除したら画面も変えるように
    // async deleteRecord() {
    //   try {
    //     const result = await axios.post("http://localhost:3000/delete");
    //     if (result.data === "OK") {
    //       // 認証に成功した場合
    //       console.log(result);
    //       console.log("認証に成功しました。");
    //     } else {
    //       // 認証に失敗した場合
    //       console.log("認証に失敗しました。");
    //     }
    //   } catch {
    //     alert("処理に失敗しました。");
    //   }
    // },
  },

  mounted() {
    this.socket = io("localhost:3000");

    // 投稿されたデータの取得
    this.socket.on("MESSAGE", (data) => {
      this.messages = [...this.messages, data];
    });
  },
};
</script>

<style scoped>
/* CSSでv-list-itemを指定する場合、下記の指定の仕方ができる。 */
.v-list-item__content {
  text-align: left;
}
</style>
