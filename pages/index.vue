<template>
  <b-container fluid>
    <b-row>
      <b-col></b-col>
      <b-col class="text-center text-light title">Gakicho</b-col>
      <b-col>
        <b-button variant="info" @click="penToggle">Pen</b-button>
        <b-button variant="primary" @click="download">DL</b-button>
      </b-col>
    </b-row>
    <b-row>
      <b-col class="canvasCol p-2">
        <canvas id="canvas"></canvas>
      </b-col>
    </b-row>
    <b-row>
      <b-col class="inputCol p-2">
        <b-input class="input" v-model="inputText" @keyup.enter="drawText" placeholder="text(push enter)" />
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
import { fabric } from "fabric";

export default {
  methods: {
    drawText() {
      let text = new fabric.Text(this.inputText, { left: 50, top: 50 });
      this.canvas.add(text);
    },
    penToggle() {
      this.canvas.isDrawingMode = !this.canvas.isDrawingMode;
    },
    download() {
      let link = document.createElement("a");
      link.href = canvas.toDataURL("image/png");
      link.download = new Date().getTime() + ".png";
      link.click();
    }
  },
  data() {
    return {
      canvas: null,
      target: null,
      inputText: "",
      isDown: false,
      x1: 0,
      y1: 0,
      x2: 0,
      y2: 0
    };
  },
  mounted() {
    this.canvas = new fabric.Canvas("canvas");
    this.canvas.isDrawingMode = false;
    this.canvas.freeDrawingBrush.color = "#333333";
    this.canvas.freeDrawingBrush.width = 3;
    this.canvas.backgroundColor = "#fcfcfc";
    this.canvas.setHeight("300");
    this.canvas.setWidth("400");
  }
};
</script>

<style>
.container-fluid {
  background-color: #aaaaaa;
}
.title {
  font-size: 1.5rem;
}
.canvasCol,
.inputCol {
  display: flex;
  justify-content: center;
  align-items: center;
}
.input {
  width: 400px;
}
</style>
