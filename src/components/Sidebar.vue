<template>
    <div id="sidebar">
      <ul class="selected-squares">
        <li v-bind:key="clickedSquare" v-for="clickedSquare in clickedSquares">{{ clickedSquare }}</li>
      </ul>
    </div>
</template>

<script>
export default {
  name: "Sidebar",

  props: {
    clickedSquares: { type: Array }
  }
};
</script>

<style scoped>
#sidebar {
  height: calc(100vh - 40px);
  width: 35vw;
  max-width: 400px;
  margin: 20px;
  background-color: #fff;
  text-align: left;
  overflow: scroll;
  border-radius: 3px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  font-weight: bold;
}

@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {
  #sidebar {
    height: 22.5vh;
    width: 95vw;
    background-color: #fff;
    margin: 20px 5px 5px 5px;
    text-align: left;
    overflow: scroll;
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  }
}

.selected-squares {
  color: #312e2b;
  list-style-type: none;
}
</style>
