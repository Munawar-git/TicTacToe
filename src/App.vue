<template>
  <div>
    <h1>Tic Tac Toe</h1>
    <div class="tictactoe">
      <div>
        <Box
          v-for="n in 3"
          v-bind:key="n"
          @click.once="sendShape(n)"
          :shape="shapeVal"
          :index="n"
          :win="win"
        />
      </div>
      <div>
        <Box
          v-for="n in 3"
          v-bind:key="n + 3"
          @click.once="sendShape(n + 3)"
          :shape="shapeVal"
          :index="n + 3"
          :win="win"
        />
      </div>
      <div>
        <Box
          v-for="n in 3"
          v-bind:key="n + 6"
          @click.once="sendShape(n + 6)"
          :shape="shapeVal"
          :index="n + 6"
          :win="win"
        />
      </div>
    </div>
    <h2 v-show="win">{{ win }} wins!!</h2>
  </div>
</template>

<script>
import Box from "./components/Box.vue";
export default {
  name: "App",
  data() {
    return {
      shapeVal: true,
      crossString: "",
      zeroString: "",
      win: null,
      result: true,
      winConditions: ["123", "456", "789", "147", "258", "369", "159", "357"],
    };
  },
  components: {
    Box,
  },
  methods: {
    sendShape(index) {
      this.checkString(this.shapeVal, index);
      this.shapeVal = !this.shapeVal;
      this.oldIndex = index;
    },

    checkString(value, index) {
      if (value) {
        this.crossString += String(index);
        if (this.checkWinCondition(this.crossString)) {
          this.win = "Blue";
        }
      } else {
        this.zeroString += String(index);
        if (this.checkWinCondition(this.zeroString)) {
          this.win = "Green";
        }
      }
      console.log(this.win);
    },

    checkWinCondition(checkString) {
      console.log(checkString);
      for (let i = 0; i < this.winConditions.length; i++) {
        let singleCondition = [...this.winConditions[i]];
        this.result =
          checkString.includes(singleCondition[0]) &&
          checkString.includes(singleCondition[1]) &&
          checkString.includes(singleCondition[2]);
        if (this.result) {
          return this.result;
        }
      }
      return this.result;
    },
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.tictactoe {
  display: flex;
  justify-content: center;
}
</style>
