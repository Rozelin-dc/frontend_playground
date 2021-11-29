<template>
  <div>
    <h1>Canvas</h1>
    <canvas
      id="canvas"
      @mousedown="dragStart"
      @mouseup="dragEnd"
      @mouseout="dragEnd"
      @mousemove="draw"
    />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component'

@Options({
  name: 'Two-js',
})
export default class extends Vue {
  canvas: HTMLCanvasElement | null = null
  ctx: CanvasRenderingContext2D | null = null
  beginX = 0
  beginY = 0
  endX = 0
  endY = 0

  mounted() {
    this.canvas = <HTMLCanvasElement>document.getElementById('canvas')

    if (!this.canvas) {
      return
    }

    this.canvas.width = screen.width
    this.canvas.height = screen.availHeight - 100
    this.ctx = this.canvas.getContext('2d')

    if (!this.ctx) {
      return
    }

    this.ctx.fillRect(10, 10, 10, 10)
  }

  // 描画開始（mousedown）
  dragStart(e) {
    this.beginX = e.layerX
    this.beginY = e.layerY
  }

  // 描画終了（mouseup, mouseout）
  dragEnd(e) {
    if (!this.ctx) {
      return
    }

    this.endX = e.layerX
    this.endY = e.layerY

    this.ctx.fillRect(
      this.beginX,
      this.beginY,
      this.endX - this.beginX,
      this.endY - this.beginY
    )
  }
}
</script>
