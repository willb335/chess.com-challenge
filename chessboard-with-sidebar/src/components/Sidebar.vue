<template>
    <div id="sidebar">
      <div class="selected-squares">{{ clickedSquares }}</div>
    </div>
</template>

<script>
export default {
  name: "Sidebar",
  props: {
    clickedSquares: { type: Array }
  },
  data: function() {
    return {};
  }
};
</script>

<style scoped>
#sidebar {
  height: calc(100vh - 40px);
  width: 35vw;
  max-width: 400px;
  margin: 20px;
  background-color: #111;
  display: flex;
  justify-content: flex-start;
  align-items: center;
}

@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {
  #sidebar {
    height: 22.5vh;
    width: 95vw;
    background-color: #111;
    margin: 20px 5px 5px 5px;
    display: flex;
    justify-content: flex-start;
    align-items: center;
  }
}

.selected-squares {
  color: #fff;
}
</style>
