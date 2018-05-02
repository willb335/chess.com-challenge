<template>
    <ul id="chessboard">
        <li v-bind:key="index" v-bind:class="handleClasses(square, index)" v-for="(square, index) of squares" v-on:click="handleSquareClick(index)">
          <div v-if="clickedSquare === index" class="clicked"/>
        </li>
    </ul>
</template>



<script>
import { range } from "lodash";

export default {
  name: "Chessboard",

  data: function() {
    return {
      squares: [],
      clickedSquare: -1,
      clickedSquares: [],
      numberOfClicks: 0
    };
  },

  methods: {
    handleSquareClick: function(index) {
      this.numberOfClicks++;
      this.clickedSquare = index;
      this.clickedSquares.push(
        `${this.numberOfClicks}. ${this.convertSquareToCordinate(index + 1)}`
      );
      this.$emit("handleSquareClick", this.clickedSquares);
    },

    convertSquareToCordinate: function(num) {
      const coordinates = [
        { range: range(1, 9), row: 8, col: num },
        { range: range(9, 17), row: 7, col: num - 8 },
        { range: range(17, 25), row: 6, col: num - 16 },
        { range: range(25, 33), row: 5, col: num - 24 },
        { range: range(33, 41), row: 4, col: num - 32 },
        { range: range(41, 49), row: 3, col: num - 40 },
        { range: range(49, 57), row: 2, col: num - 48 },
        { range: range(57, 65), row: 1, col: num - 56 }
      ];

      const findRow = coordinates.find(({ range }) => range.includes(num));

      const convertColumnsToLetters = col => {
        switch (col) {
          case 1:
            return "a";
          case 2:
            return "b";
          case 3:
            return "c";
          case 4:
            return "d";
          case 5:
            return "e";
          case 6:
            return "f";
          case 7:
            return "g";
          case 8:
            return "h";
          default:
            return null;
        }
      };

      return `${convertColumnsToLetters(findRow.col)}${findRow.row} `;
    },

    handleClasses: function(square, index) {
      if (index === 0) {
        return square === "odd"
          ? `odd square top-left`
          : `even square top-left`;
      }

      if (index === 7) {
        return square === "odd"
          ? `odd square top-right`
          : `even square top-right`;
      }

      if (index === 56) {
        return square === "odd"
          ? `odd square bottom-left`
          : `even square bottom-left`;
      }

      if (index === 63) {
        return square === "odd"
          ? `odd square bottom-right`
          : `even square bottom-right`;
      }

      return square === "odd" ? `odd square` : `even square`;
    }
  },

  created: function() {
    let row = 1;
    return [...Array(64)].forEach((s, i) => {
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
li {
  flex-basis: 12.5%;
}

li:nth-child(even).even {
  background: #8876b7;
}

li:nth-child(odd).even {
  background: #efefef;
}

li:nth-child(even).odd {
  background: #efefef;
}

li:nth-child(odd).odd {
  background: #8876b7;
}

.square {
  position: relative;
  list-style-type: none;
}

.clicked {
  position: absolute;
  background-color: rgba(247, 247, 115, 0.6);
  width: 100%;
  height: 100%;
}

.top-left {
  border-top-left-radius: 3px;
}

.top-right {
  border-top-right-radius: 3px;
}

.bottom-left {
  border-bottom-left-radius: 3px;
}

.bottom-right {
  border-bottom-right-radius: 3px;
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
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
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
