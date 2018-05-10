<template>
    <ul id="chessboard">
        <li v-bind:key="index" tabindex="0" v-bind:class="handleSquareClasses(square, index)" v-for="(square, index) of squares" v-on:click="handleSquareClick(index)" v-on:keyup.enter="handleSquareClick(index)" v-on:keydown="handleArrowKeys($event, index)">
          <div v-if="selectedSquare === index" class="clicked"/>
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
      selectedSquares: [],
      selectedSquare: -1,
      numberOfClicks: 0
    };
  },

  methods: {
    /**
     * Makes chessboard keyboard accesible via arrow keys
     * @param {Event} e - the event object
     * @param {number} index - index of square
     * @returns {void}
     */
    handleArrowKeys: function(e, index) {
      //up
      if (e.keyCode === 38) {
        document.getElementsByClassName((index - 8).toString())[0].focus();
      }
      //down
      if (e.keyCode === 40) {
        document.getElementsByClassName((index + 8).toString())[0].focus();
      }
      //right
      if (e.keyCode === 39) {
        document.getElementsByClassName((index + 1).toString())[0].focus();
      }
      //left
      if (e.keyCode === 37) {
        document.getElementsByClassName((index - 1).toString())[0].focus();
      }
    },
    /**
     * Records the selectedSquare and adds it to the array of selectedSquares.  Also emits this.selectedSquares to App
     * @param {number} index - index of square
     * @returns {void}
     */
    handleSquareClick: function(index) {
      this.numberOfClicks++;
      this.selectedSquare = index;
      this.selectedSquares.push(
        `${this.numberOfClicks}. ${this.convertSquareToCordinate(index + 1)}`
      );
      this.$emit("handleSquareClick", this.selectedSquares);
    },
    /**
     * Sets square to a coordinate, i.e. 1 is set to a8
     * @param {number} num - the number of the square, ranges from 1-65(not including 65)
     * @returns {string} - the coordinate to be output in the Sidebar
     */
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

      const findCoordinate = coordinates.find(({ range }) =>
        range.includes(num)
      );

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

      return `${convertColumnsToLetters(findCoordinate.col)}${
        findCoordinate.row
      }`;
    },
    /**
     * Handles css classes, notably the corner squares' border-radii
     * @param {string} square - the initial value of each square. If odd, square is "odd" and if even, square is "even"
     * @param {number} index - index of this.squares
     * @returns {string} - the css classes
     */
    handleSquareClasses: function(square, index) {
      if (index === 0) {
        return square === "odd"
          ? `odd square top-left ${index}`
          : `even square top-left ${index}`;
      }

      if (index === 7) {
        return square === "odd"
          ? `odd square top-right ${index}`
          : `even square top-right ${index}`;
      }

      if (index === 56) {
        return square === "odd"
          ? `odd square bottom-left ${index}`
          : `even square bottom-left ${index}`;
      }

      if (index === 63) {
        return square === "odd"
          ? `odd square bottom-right ${index}`
          : `even square bottom-right ${index}`;
      }

      return square === "odd" ? `odd square ${index}` : `even square ${index}`;
    }
  },
  /**
   * Creates an array of 64 items that populate the <li/>
   * @returns {void}
   */
  created: function() {
    let row = 1;
    [...Array(64)].forEach((_, i) => {
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

.square:focus {
  z-index: 5;
  outline: 2px solid rgba(255, 239, 153, 1);
  outline-offset: -2px;
}

.clicked {
  position: absolute;
  background-color: rgba(255, 239, 153, 0.6);
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
  align-self: center;
  margin-right: 20px;
  padding: 0;
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.5);
}

@media only screen and (min-device-width: 320px) and (max-device-width: 600px) {
  #chessboard {
    width: 95vw;
    height: 95vw;
    margin: 10px 0 0 0;
  }
}
</style>
