<template>
  <div id="app">
    <upload-container />
  </div>
</template>

<script>
import UploadContainer from "./components/UploadContainer.vue";

export default {
  name: "app",
  components: {
    UploadContainer
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
  display: flex;
  align-items: center;
  justify-content: center;
}
</style>
