<template>
  <div id="app">
    <zip-demo msg="vue zip files preview demo"></zip-demo>
  </div>
</template>

<script>
import zipDemo from "./components/zipDemo";

export default {
  name: "app",
  components: {
    zipDemo
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
