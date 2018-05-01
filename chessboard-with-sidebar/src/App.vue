<template>
  <div id="app">
    <div class="flex-container">
      <Chessboard msg="Chessboard goes here!"/>
    </div>
  </div>
</template>

<script>
import Chessboard from "./components/Chessboard.vue";
export default {
  name: "app",
  components: {
    Chessboard
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
  height: 100vh;
  border: 1px solid red;
}

.flex-container {
  border: 1px solid blue;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
}
</style>
