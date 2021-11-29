<template>
  <div>
    <h1>Canvas</h1>
    <canvas id="canvas" />
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

  mounted() {
    this.canvas = <HTMLCanvasElement>document.getElementById('canvas')

    if (!this.canvas) {
      return
    }

    this.ctx = this.canvas.getContext('2d')
    this.ctx?.fillRect(10, 10, 10, 10)
  }
}
</script>
