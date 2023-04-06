<template>
  <button
    class="box"
    :class="{ blue: colorClass && color, green: colorClass && !color }"
    @click="onClick"
    :disabled="win"
  >
    <!-- {{ index }} -->
    <p class="sign" v-show="colorClass && color">X</p>
    <p class="sign" v-show="colorClass && !color">O</p>
  </button>
</template>

<script>
export default {
  name: "Box",
  data() {
    return {
      isClicked: false,
      colorClass: false,
      color: false,
    };
  },
  props: { shape: { type: Boolean }, index: Number, win: String },

  methods: {
    onClick() {
      if (!this.isClicked) {
        this.colorClass = true;
        this.color = this.shape;
        this.isClicked = true;
      }
    },
  },
};
</script>

<style>
.box {
  display: block;
  height: 50px;
  width: 50px;
  border: 2px solid red;
  background: yellow;
  cursor: pointer;
}
.box.blue {
  background: blue;
}
.box.green {
  background: green;
}
.sign {
  color: white;
  font-weight: bolder;
  font-size: 1.25rem;
}
</style>