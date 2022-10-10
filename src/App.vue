<template>
  <img alt="Vue logo" src="./assets/hibixby.jpg" />
  <div>
    <h1>{{ name }}</h1>
  </div>
  <form>
    <input type="text"/>
    <button type="submit">보내기</button>

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
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
