<template>
  <!-- Success alert -->
  <CustomAlert
    v-bind:success="success"
    @dismissAlert="dismissAlert"
  ></CustomAlert>

  <!-- Logo -->
  <HeadLine v-bind:owner="owner"></HeadLine>
  <hr />

  <!-- form -->
  <form v-on:submit.prevent="sendMessage">
    <div class="px-3 py-3">
      <!-- text inputs start -->
      <div v-for="inputConfig in inputConfigs" :key="inputConfig">
        <label
          v-bind:ref_for="inputConfig.id"
          class="block text-sm font-medium text-slate-700"
        >
          {{ inputConfig.label }}
        </label>
        <input
          v-bind:id="inputConfig.id"
          type="text"
          class="peer mt-1 px-3 py-2 bg-white border shadow-sm border-slate-300 placeholder-slate-400 focus:outline-none focus:border-sky-500 focus:ring-sky-500 block w-full rounded-md sm:text-sm focus:ring-1"
          v-model.lazy="name"
          required
          v-bind:placeholder="inputConfig.placeholder"
        />
        <p class="mt-2 invisible peer-invalid:visible text-pink-600 text-sm">
          {{ inputConfig.invalid }}
        </p>
      </div>

      <input
        id="remember"
        type="checkbox"
        v-model="remember"
        v-on:change="rememberMe"
        class="checked:bg-blue-500 ..."
      />
      <label for="remember" class="">이름 기억하기 - WIP</label>
      <br />
      <button
        type="submit"
        class="rounded-lg p-2 text-white bg-gradient-to-r from-green-400 to-blue-500 hover:from-pink-500 hover:to-yellow-500 active:bg-sky-700 focus:outline-none focus:ring focus:ring-sky-300 w-full"
      >
        <i class="fa-solid fa-paper-plane"></i> 보내기
      </button>
    </div>
  </form>
</template>

<script>
import axios from "axios";
import CustomAlert from "./components/CustomAlert.vue";
import HeadLine from "./components/HeadLine.vue";
export default {
  name: "App",
  data() {
    return {
      owner: "HiBixby",
      remember: false,
      success: false,
      failure: false,
      inputConfigs: [
        {
          label: "이름",
          id: "name",
          placeholder: "ex) 홍길동",
          invalid: "이름을 입력해주세요.",
        },
        {
          label: "내용",
          id: "context",
          placeholder: "ex) 답장 부탁드립니다.",
          invalid: "내용을 입력해주세요.",
        },
      ],
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

#app {
  font-family: "Pretendard", -apple-system, BlinkMacSystemFont, system-ui,
    Roboto, "Helvetica Neue", "Segoe UI", "Apple SD Gothic Neo", "Noto Sans KR",
    "Malgun Gothic", sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
