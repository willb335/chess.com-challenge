<template>
    <ul id="chessboard">
        <li v-bind:class="[(square === 'odd') ? `odd square ${generatedClass[index]}` : `even square ${generatedClass[index]}`]" v-for="(square, index) of squares" v-bind:key="index" v-on:click="handleSquareClick(index)">
          <div v-if="clickedSquare === index" class="clicked">
          </div>
          <div v-else></div>
        </li>
    </ul>
</template>



<script>
export default {
  name: "Chessboard",
  data: function() {
    return {
      squares: [],
      indexes: [],
      clickedSquare: "none",
      clickedSquares: []
    };
  },
  computed: {
    generatedClass: function() {
      return this.indexes.map((n, i) => "square" + "-" + (i + 1));
    }
  },
  methods: {
    handleSquareClick: function(index) {
      this.clickedSquare = index;
      this.clickedSquares.push(index + 1);
      this.$emit("handleSquareClick", this.clickedSquares);
    }
  },
  created: function() {
    let row = 1;
    this.indexes = Array(64).fill(0);
    return Array(64)
      .fill(0)
      .forEach((s, i) => {
        if (i % 8 === 0) row = row + 1;

        if (row % 2 === 0) {
          this.squares.push("even");
        } else {
          this.squares.push("odd");
        }
      });
  }
};
</script>

<style scoped>
li:nth-child(even).even {
  background: #8876b7;
  flex-basis: 12.5%;
}

li:nth-child(odd).even {
  background: #efefef;
  flex-basis: 12.5%;
}

li:nth-child(even).odd {
  background: #efefef;
  flex-basis: 12.5%;
}

li:nth-child(odd).odd {
  background: #8876b7;
  flex-basis: 12.5%;
}

.square {
  position: relative;
  list-style-type: none;
}

.clicked {
  position: absolute;
  outline: 3px solid green;
  width: calc(100% - 6px);
  height: calc(100% - 6px);
  left: 3px;
  top: 3px;
  mright: 3px;
  bottom: 3px;
}

#chessboard {
  display: flex;
  justify-content: stretch;
  align-items: stretch;
  max-height: 85vh;
  max-width: 85vh;
  width: calc(85vw - 35vw);
  height: calc(85vw - 35vw);
  flex-wrap: wrap;
  padding: 0px;
  align-self: center;
  margin-right: 20px;
}

@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {
  #chessboard {
    display: flex;
    justify-content: stretch;
    align-items: stretch;
    width: 95vw;
    height: 95vw;
    flex-wrap: wrap;
    padding: 0px;
    margin: 0px;
  }
}
</style>
