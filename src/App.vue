<template>

  <!-- Success alert -->
  <div class="alert-container w-full px-5">
    <div class="bg-green-100 rounded-lg py-5 px-6 mb-3 text-base text-green-700 inline-flex items-center w-full"
      role="alert">
      <svg aria-hidden="true" focusable="false" data-prefix="fas" data-icon="check-circle"
        class="w-4 h-4 mr-2 fill-current" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512">
        <path fill="currentColor"
          d="M504 256c0 136.967-111.033 248-248 248S8 392.967 8 256 119.033 8 256 8s248 111.033 248 248zM227.314 387.314l184-184c6.248-6.248 6.248-16.379 0-22.627l-22.627-22.627c-6.248-6.249-16.379-6.249-22.628 0L216 308.118l-70.059-70.059c-6.248-6.248-16.379-6.248-22.628 0l-22.627 22.627c-6.248 6.248-6.248 16.379 0 22.627l104 104c6.249 6.249 16.379 6.249 22.628.001z">
        </path>
      </svg>
      메세지 전송 성공! - 아직 작업중인 페이지 입니다.
    </div>
  </div>

  <!-- Logo -->

  <img class="mx-auto rounded-full border-slate-300 border-2" alt="HiBixby Logo" src="./assets/hibixby.jpg" />

  <div>
    <h1 class="font-bold text-3xl">{{ name }}</h1>
  </div>
  <h4>HiBixby에게 Discord 알림 보내기</h4>
  <hr />
  <br />
  <form>
    <label class="block">
      <span class="block text-sm font-medium text-slate-700">내용</span>
      <div class="px-3">
        <input type="text"
          class="peer mt-1 px-3 py-2 bg-white border shadow-sm border-slate-300 placeholder-slate-400 focus:outline-none focus:border-sky-500 focus:ring-sky-500 block w-full rounded-md sm:text-sm focus:ring-1"
          placeholder="안녕하세요!" />
      </div>
      <p class="mt-2 invisible peer-invalid:visible text-pink-600 text-sm">
        내용을 입력해주세요.
      </p>
    </label>
    <button type="submit"
      class="rounded-lg p-2 text-white bg-violet-500 hover:bg-violet-600 active:bg-violet-700 focus:outline-none focus:ring focus:ring-violet-300">보내기</button>
  </form>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      name: "HiBixby",
    };
  },
  components: {},
};
</script>

<style>
@import url('https://cdn.jsdelivr.net/gh/orioncactus/pretendard/dist/web/static/pretendard-dynamic-subset.css');

#app {

  font-family: 'Pretendard', -apple-system, BlinkMacSystemFont, system-ui, Roboto, 'Helvetica Neue', 'Segoe UI', 'Apple SD Gothic Neo', 'Noto Sans KR', 'Malgun Gothic', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
