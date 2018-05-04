<template>
    <div id="sidebar">
      <ul class="selected-squares">
        <div class="row">
          <li v-bind:key="selectedSquare" v-for="selectedSquare of selectedSquares">{{ selectedSquare }}</li>
        </div>
      </ul>
    </div>
</template>

<script>
export default {
  name: "Sidebar",

  props: {
    selectedSquares: { type: Array }
  }
};
</script>

<style scoped>
#sidebar {
  height: calc(100vh - 40px);
  width: 35vw;
  max-width: 400px;
  margin: 10px;
  background-color: #fff;
  overflow: scroll;
  border-radius: 3px;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
  font-weight: bold;
}

.selected-squares {
  color: #312e2b;
  list-style-type: none;
  display: contents;
}

.row {
  display: flex;
  justify-content: flex-start;
  align-items: flex-start;
  flex-wrap: wrap;
  width: 100%;
  padding: 10px 5px 10px 5px;
}

li {
  flex-basis: calc(20% - 5px);
}

@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {
  #sidebar {
    height: 24vh;
    width: 95vw;
    max-width: 95vw;
    overflow-y: scroll;
    overflow-x: hidden;
  }

  .row {
    width: calc(95vw - 20px);
  }

  li {
    flex-basis: 16.66%;
    font-size: 12px;
  }
}

@media only screen and (min-device-width: 600px) and (max-device-width: 1024px) {
  li {
    flex-basis: 30%;
  }
}
</style>
