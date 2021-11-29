<template>
  <div>
    <h1>Two.js</h1>
    <div id="playground" />
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

  async mounted() {
    this.element = document.getElementById('playground')

    if (!this.element) {
      return
    }

    this.two = new Two().appendTo(this.element)
    try {
      this.circle = await this.two.makeCircle(110, 110, 50)
      await (this.circle.fill = '#FF8039')
    } finally {
      this.two.update()
    }
  }
}
</script>
