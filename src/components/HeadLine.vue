<template>
  <img
    class="mx-auto rounded-full border-slate-300 border-2"
    width="100"
    alt="HiBixby Logo"
    src="../assets/hibixby.jpg"
  />

  <div>
    <h1 class="font-bold text-3xl">{{ owner }}</h1>
  </div>
  <h4>HiBixby에게 Discord 알림 보내기</h4>
  <hr />
  <br />
</template>

<script>
export default {
  name: "HeadLine",
  props: {
    owner: String,
  },
  methods: {},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
