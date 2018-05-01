<template>
  <div id="app">
    <div class="flex-container">
      <Chessboard msg="Chessboard goes here!"/>
      <Sidebar/>
    </div>
  </div>
</template>

<script>
import Chessboard from "./components/Chessboard.vue";
import Sidebar from "./components/Sidebar.vue";
export default {
  name: "app",
  components: {
    Chessboard,
    Sidebar
  }
};
</script>

<style>
body {
  overflow: hidden;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.flex-container {
  background-color: purple;
  float: left;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  width: 100vw;
}
</style>
