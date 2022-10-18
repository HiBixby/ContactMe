<template>
  <div class="my-5 text-center">
    <img
      class="mx-auto rounded-full border-slate-300 border-2 w-28"
      alt="HiBixby의 프로필 이미지"
      src="../assets/hibixby.jpg"
    />

    <div>
      <h1 class="font-bold text-3xl">{{ owner }}</h1>
    </div>
    <p>{{owner}}에게 <i class="fa-brands fa-discord"></i>Discord 알림 보내기</p>
  </div>
</template>

<script>
export default {
  name: "HeadLine",
  props: {
  },
  data(){
    return{
      owner:"HiBixby",
    };
  },
  methods: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
