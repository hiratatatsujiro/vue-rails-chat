<template>
  <div class="container">
    <NavbarPage />
    <ChatWindow :messages="messages" />
  </div>
</template>

<script>
import NavbarPage from "../components/NavbarPage.vue";
import ChatWindow from "../components/ChatWindow.vue";
import axios from "axios"

export default {
    components: { NavbarPage, ChatWindow },
    data() {
      return {
       messages: []
      }
    },
    methods: {
      async getMessages () {
        try {
          const res = await axios.get("http://localhost:3000/messages", {
            uid: window.sessionStorage.getItem("uid"),
            "access-token": window.sessionStorage.getItem("access-token"),
            client: window.sessionStorage.getItem("client")
          })
          if (!res) {
            new Error("メッセージ一覧を取得できませんでした")
          }
          this.messages = res.data
        } catch(err) {
          console.log(err)
        }
      },
    },
    mounted() {
      this.getMessages()
    },
}
</script>

<style scoped>
</style>