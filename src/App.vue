<template>
  <div class="min-h-full flex flex-col">
    <!-- Success alert -->
    <CustomAlert
      v-bind:success="success"
      @dismissAlert="dismissAlert"
      class="flex-none"
    ></CustomAlert>

    <!-- Logo -->
    <HeadLine class="flex-none"></HeadLine>
    <hr />

    <!-- form -->
    <form v-on:submit.prevent="sendMessage" class="flex-1 flex">
      <div class="w-full px-10 py-10 flex flex-col">
        <!-- text inputs start -->
        <label
          ref_for="name"
          class="after:content-['*'] after:ml-0.5 after:text-red-500 block font-medium text-slate-700"
        >
          이름
        </label>
        <input
          id="name"
          type="text"
          class="peer mt-1 px-3 py-2 bg-white border shadow-sm border-slate-300 placeholder-slate-400 focus:outline-none focus:border-sky-500 focus:ring-sky-500 block w-full rounded-md focus:ring-1 invalid:border-pink-500 invalid:text-pink-600 focus:invalid:border-pink-500 focus:invalid:ring-pink-500"
          v-model.lazy="name"
          required
          placeholder="ex) 홍길동"
          title="이름을 입력하세요"
          alt="이름 입력 박스"
        />
        <p class="mt-2 invisible peer-invalid:visible text-pink-600 text-sm">
          이름을 입력해주세요.
        </p>
        <label
          ref_for="message"
          class="after:content-['*'] after:ml-0.5 after:text-red-500 block font-medium text-slate-700"
        >
          전달할 메세지
        </label>
        <textarea
          id="message"
          class="flex-1 peer mt-1 px-3 py-2 bg-white border shadow-sm border-slate-300 placeholder-slate-400 focus:outline-none focus:border-sky-500 focus:ring-sky-500 block w-full rounded-md focus:ring-1 invalid:border-pink-500 invalid:text-pink-600 focus:invalid:border-pink-500 focus:invalid:ring-pink-500"
          v-model.lazy="message"
          required
          title="전달할 메세지를 입력하세요"
          alt="전달할 메세지 입력 박스"
        ></textarea>
        <p class="mt-2 invisible peer-invalid:visible text-pink-600">
          전달할 메세지를 입력해주세요.
        </p>
        <br />
        <div class="기억하기">
          <input
            id="remember"
            type="checkbox"
            v-model="remember"
            v-on:change="rememberMe"
            class="checked:bg-blue-500 mr-2"
            alt="이름 기억하기 체크박스"
          />
          <label for="remember" class="">이름 기억하기</label>
        </div>
        <br />
        <button
          type="submit"
          class="rounded-lg p-2 text-white bg-gradient-to-r from-green-400 to-blue-500 hover:from-pink-500 hover:to-yellow-500 active:bg-sky-700 focus:outline-none focus:ring focus:ring-sky-300 w-full h-12 text-lg"
          alt="보내기 버튼"
        >
          <i class="fa-solid fa-paper-plane"></i> 보내기
        </button>
      </div>
    </form>
  </div>
</template>

<script>
/* eslint-disable */
import axios from "axios";
import CustomAlert from "./components/CustomAlert.vue";
import HeadLine from "./components/HeadLine.vue";

export default {
  name: "App",
  data() {
    return {
      remember: localStorage.getItem("name") ? true : false,
      success: false,
      failure: false,
      name: localStorage.getItem("name") ? localStorage.getItem("name") : "",
      message: "",
    };
  },
  components: { CustomAlert, HeadLine },
  methods: {
    dismissAlert: function () {
      console.log("dismiss alert!");
      this.success = false;
    },
    rememberMe: function () {
      console.log(this.remember);
      if (this.remember) {
        localStorage.setItem("name", this.name);
      } else {
        localStorage.clear("name");
      }
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
              value: this.message,
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
          this.message = "";
        })
        .catch((err) => {
          console.log(err);
          console.log("웹후크 전달 실패");
          this.success = false;
          this.failure = true;
          alert("실패");
        });
    },
  },
};
</script>

<style>
@import url("https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard-dynamic-subset.css");
html,
body {
  height: 100%;
  margin: 0px;
}
#app {
  font-family: "Pretendard", -apple-system, BlinkMacSystemFont, system-ui,
    Roboto, "Helvetica Neue", "Segoe UI", "Apple SD Gothic Neo", "Noto Sans KR",
    "Malgun Gothic", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  height: 100%;
}
</style>
