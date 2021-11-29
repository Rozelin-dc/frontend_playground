<template>
  <div>
    <h1>Two.js</h1>
    <svg id="playground" />
  </div>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component'
import Two from 'twojs-ts'

@Options({
  name: 'Two-js',
})
export default class extends Vue {
  element: HTMLElement | null = null
  two: Two | null = null
  circle: Two.Circle | null = null

  mounted() {
    this.element = document.getElementById('playground')

    if (!this.element) {
      return
    }

    this.two = new Two().appendTo(this.element)
    this.circle = this.two.makeCircle(0, 0, 50)
    // this.circle.fill = '#FF8000'
    this.two.update()
  }
}
</script>
