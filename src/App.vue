<template>
  <div id="app">
    <div class="flex-container">
      <Chessboard v-on:handleSquareClick="storeSelectedSquares($event)"/>
      <Sidebar v-bind:selected-squares="selectedSquares"/>
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
      selectedSquares: []
    };
  },

  methods: {
    /**
     * Sets this.selectedSquares, which is passed to Sidebar
     * @param {Array<String>} selectedSquares - An array of coordinates.
     * @returns {void}
     */
    storeSelectedSquares: function(selectedSquares) {
      this.selectedSquares = selectedSquares;
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
  background-color: #e0e0e0;
}

@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {
  .flex-container {
    flex-direction: column;
    justify-content: center;
  }
}
</style>
