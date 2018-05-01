<template>
    <div id="sidebar">
      <div>{{ clickedSquares }}</div>
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
  height: 95vh;
  width: 22.5vw;
  background-color: #111;
  margin: 20px 20px 20px 40px;
  display: flex;
  justify-content: flex-start;
  align-items: center;
}

@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {
  #sidebar {
    height: 22.5vh;
    width: 95vw;
    background-color: #111;
    margin: 20px 20px 20px 20px;
    display: flex;
    justify-content: flex-start;
    align-items: center;
  }
}

@media only screen and (min-device-width: 480px) and (max-device-width: 900px) and (orientation: landscape) {
  #sidebar {
    height: 95vh;
    width: 22.5vh;
    background-color: #111;
    display: flex;
    justify-content: flex-start;
    align-items: center;
  }
}
</style>
