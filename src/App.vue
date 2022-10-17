<template>
  <!-- Success alert -->
  <div class="alert-container w-full px-5">
    <div
      :class="{ hidden: !success }"
      class="bg-green-100 rounded-lg py-5 px-6 mb-3 text-base text-green-700 inline-flex items-center w-full"
      role="alert"
    >
      <svg
        aria-hidden="true"
        focusable="false"
        data-prefix="fas"
        data-icon="check-circle"
        class="w-4 h-4 mr-2 fill-current"
        role="img"
        xmlns="http://www.w3.org/2000/svg"
        viewBox="0 0 512 512"
      >
        <path
          fill="currentColor"
          d="M504 256c0 136.967-111.033 248-248 248S8 392.967 8 256 119.033 8 256 8s248 111.033 248 248zM227.314 387.314l184-184c6.248-6.248 6.248-16.379 0-22.627l-22.627-22.627c-6.248-6.249-16.379-6.249-22.628 0L216 308.118l-70.059-70.059c-6.248-6.248-16.379-6.248-22.628 0l-22.627 22.627c-6.248 6.248-6.248 16.379 0 22.627l104 104c6.249 6.249 16.379 6.249 22.628.001z"
        ></path>
      </svg>
      메세지 전송 성공!
      <button v-on:click="dismissAlert" class="ml-auto">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="fill-current text-gray-700"
          viewBox="0 0 16 16"
          width="20"
          height="20"
        >
          <path
            fill-rule="evenodd"
            d="M3.72 3.72a.75.75 0 011.06 0L8 6.94l3.22-3.22a.75.75 0 111.06 1.06L9.06 8l3.22 3.22a.75.75 0 11-1.06 1.06L8 9.06l-3.22 3.22a.75.75 0 01-1.06-1.06L6.94 8 3.72 4.78a.75.75 0 010-1.06z"
          ></path>
        </svg>
      </button>
    </div>
  </div>

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
export default {
  name: "App",
  data() {
    return {
      owner: "HiBixby",
      success: false,
    };
  },
  components: {},
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
