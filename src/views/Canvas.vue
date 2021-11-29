<template>
  <div>
    <h1>Canvas</h1>
    <el-button type="danger" :icon="deleteIcon" circle @click="clear" />
    <canvas
      id="canvas"
      @mousedown="dragStart"
      @mouseup="dragEnd"
      @mouseout="dragEnd"
    />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component'
import { Delete } from '@element-plus/icons'

@Options({
  name: 'Two-js',
})
export default class extends Vue {
  deleteIcon = Delete
  canvas: HTMLCanvasElement | null = null
  ctx: CanvasRenderingContext2D | null = null
  beginX = 0
  beginY = 0
  endX = 0
  endY = 0
  isDrag = false

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
  dragStart(e: any) {
    this.beginX = e.layerX
    this.beginY = e.layerY
    this.isDrag = true
  }

  // 描画終了（mouseup, mouseout）
  dragEnd(e: any) {
    if (!this.ctx || !this.isDrag) {
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
    this.isDrag = false
  }

  clear() {
    this.ctx?.clearRect(
      0,
      0,
      this.canvas?.width as number,
      this.canvas?.height as number
    )
  }
}
</script>
