<template>
    <ul id="chessboard">
        <li v-bind:class="[(square === 'odd') ? 'odd square' : 'even square']" v-for="(square, index) of squares" v-bind:key="index">
        Hi
        </li>
    </ul>
    <!-- <h1>{{ msg }}</h1> -->
</template>



<script>
export default {
  name: "Chessboard",
  props: {
    msg: String
  },
  data: function() {
    return {
      squares: []
    };
  },
  created: function() {
    let row = 1;
    return Array(64)
      .fill(0)
      .forEach((s, i) => {
        if (i % 8 === 0) row = row + 1;

        if (row % 2 === 0) {
          this.squares.push(i + 1);
        } else {
          this.squares.push("odd");
        }
      });
  }
};
</script>

<style scoped>
#chessboard {
  display: flex;
  justify-content: stretch;
  align-items: stretch;
  width: 40vw;
  height: 40vw;
  flex-wrap: wrap;
  padding: 0px;
  margin: 0px;
}

li:nth-child(even).even {
  background: orange;
  flex-basis: 12.5%;
}

li:nth-child(odd).even {
  background: #a5673f;
  flex-basis: 12.5%;
}

li:nth-child(even).odd {
  background: #a5673f;
  flex-basis: 12.5%;
}

li:nth-child(odd).odd {
  background: orange;
  flex-basis: 12.5%;
}

.square {
  list-style-type: none;
}
</style>
