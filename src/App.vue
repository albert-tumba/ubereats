<template>
  <div class="app">
    <Home />
  </div>
</template>

<script>
import Home from "./page/home.vue";
export default {
  name: "App",
  components: {
    Home,
  },
};
</script>

<style lang="scss">
@import url("./style/reset.css");
@import url("https://fonts.googleapis.com/css2?family=Roboto&display=swap");
#app {
  font-family: "Roboto", sans-serif;
  //padding: 0px 40px;
}
</style>
