<template>
  <!-- Success alert -->
  <CustomAlert
    v-bind:success="success"
    @dismissAlert="dismissAlert"
  ></CustomAlert>

  <!-- Logo -->

  <img
    class="mx-auto rounded-full border-slate-300 border-2"
    width="100"
    alt="HiBixby Logo"
    src="./assets/hibixby.jpg"
  />

  <div>
    <h1 class="font-bold text-3xl">{{ owner }}</h1>
  </div>
  <h4>HiBixby에게 Discord 알림 보내기</h4>
  <hr />
  <br />
  <!-- form -->
  <form v-on:submit.prevent="sendMessage">
    <div class="px-3">
      <label for="name" class="block text-sm font-medium text-slate-700">
        이름
      </label>
      <input
        id="name"
        type="text"
        class="peer mt-1 px-3 py-2 bg-white border shadow-sm border-slate-300 placeholder-slate-400 focus:outline-none focus:border-sky-500 focus:ring-sky-500 block w-full rounded-md sm:text-sm focus:ring-1"
        v-model.lazy="name"
        required
        placeholder="홍길동"
      />
      <p class="mt-2 invisible peer-invalid:visible text-pink-600 text-sm">
        이름을 입력해주세요.
      </p>
    </div>
    <div class="px-3">
      <label for="content" class="block text-sm font-medium text-slate-700"
        >내용</label
      >
      <input
        id="content"
        type="text"
        class="peer mt-1 px-3 py-2 bg-white border shadow-sm border-slate-300 placeholder-slate-400 focus:outline-none focus:border-sky-500 focus:ring-sky-500 block w-full rounded-md sm:text-sm focus:ring-1"
        autocomplete="off"
        v-model.lazy="content"
        placeholder="안녕하세요!"
        required
      />

      <p class="mt-2 invisible peer-invalid:visible text-pink-600 text-sm">
        내용을 입력해주세요.
      </p>
    </div>
    <button
      type="submit"
      class="rounded-lg p-2 text-white bg-sky-500 hover:bg-sky-600 active:bg-sky-700 focus:outline-none focus:ring focus:ring-sky-300"
    >
      <i class="fa-solid fa-paper-plane"></i> 보내기
    </button>
  </form>
</template>

<script>
import axios from "axios";
import CustomAlert from "./components/CustomAlert.vue";
export default {
  name: "App",
  data() {
    return {
      owner: "HiBixby",
      success: false,
    };
  },
  components: { CustomAlert },
  methods: {
    dismissAlert: function () {
      console.log("dismiss alert!");
      this.success = false;
    },
    sendMessage: function () {
      console.log("[Send Message] : Called!");
      let embeds = [
        {
          title: "Contact Me (Vue.js)",
          timestamp: new Date(),
          color: 1752220,
          footer: {
            text: `👤${this.name}`,
          },
          fields: [
            {
              name: "내용",
              value: this.content,
            },
          ],
        },
      ];
      let data = JSON.stringify({ embeds });
      const webhook = process.env.VUE_APP_WEBHOOK_URL;
      var config = {
        method: "POST",
        url: webhook,
        headers: { "Content-Type": "application/json" },
        data: data,
      };
      axios(config)
        .then((res) => {
          console.log(res);
          console.log("웹후크 전달 성공");
          this.success = true;
          this.content = "";
        })
        .catch((err) => {
          console.log(err);
          console.log("웹후크 전달 실패");
          alert("실패");
        });
    },
  },
};
</script>

<style>
@import url("https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard-dynamic-subset.css");

#app {
  font-family: "Pretendard", -apple-system, BlinkMacSystemFont, system-ui,
    Roboto, "Helvetica Neue", "Segoe UI", "Apple SD Gothic Neo", "Noto Sans KR",
    "Malgun Gothic", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
