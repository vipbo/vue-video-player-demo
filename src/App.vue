<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
    <MVideo />
    <Progress />
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import MVideo from "./components/MVideo.vue";
import Progress from "./components/Progress.vue";

export default {
  name: "app",
  components: {
    HelloWorld,
    MVideo,
    Progress
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
