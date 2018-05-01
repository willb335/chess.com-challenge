<template>
  <div id="app">
    <div class="flex-container">
      <Chessboard msg="Chessboard goes here!" v-on:handleSquareClick="storeClickedSquares($event)"/>
      <Sidebar v-bind:clicked-squares="clickedSquares"/>
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
  },
  data: function() {
    return {
      clickedSquares: []
    };
  },
  methods: {
    storeClickedSquares: function(clickedSquares) {
      this.clickedSquares = clickedSquares;
    }
  }
};
</script>

<style>
body {
  position: relative;
  margin: 0;
  padding: 0;
  overflow: hidden;
  height: 100vh;
  width: 100vw;
  background-color: purple;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.flex-container {
  position: absolute;
  background-color: purple;
  float: left;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100%;
  width: 100%;
}

@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {
  .flex-container {
    position: absolute;
    background-color: purple;
    float: left;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: center;
    height: 100%;
    width: 100%;
  }
}
</style>
