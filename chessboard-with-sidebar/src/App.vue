<template>
  <div id="app">
    <div class="flex-container" :style="{ backgroundImage: `url('${backgroundImage}')` }">
      <Chessboard v-on:handleSquareClick="storeClickedSquares($event)"/>
      <Sidebar v-bind:clicked-squares="clickedSquares"/>
    </div>
  </div>
</template>

<script>
import Chessboard from "./components/Chessboard.vue";
import Sidebar from "./components/Sidebar.vue";
import backgroundImage from "./assets/wood.jpg";
export default {
  name: "app",

  components: {
    Chessboard,
    Sidebar
  },

  data: function() {
    return {
      clickedSquares: [],
      backgroundImage
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
  display: flex;
  justify-content: flex-end;
  align-items: center;
  height: 100%;
  width: 100%;
}

@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {
  .flex-container {
    position: absolute;
    display: flex;
    flex-direction: column;
    justify-content: flex-end;
    align-items: center;
    height: 100%;
    width: 100%;
  }
}
</style>
