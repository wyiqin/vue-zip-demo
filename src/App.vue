<template>
  <div id="app">
    <imagef msg="vue zip file"/>
    <audiof></audiof>
  </div>
</template>

<script>
import imagef from "./components/image";
import audiof from "./components/audio";

export default {
  name: "app",
  components: {
    imagef,
    audiof
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
