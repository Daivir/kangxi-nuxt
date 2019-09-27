<template>
  <v-img class="ParallaxElement" src="https://picsum.photos/1280/720" :aspect-ratio="16/9" :style="{ transform: `translate3d(0, ${offset}px, 0)` }">
    <!--  <div
    :style="{ transform: `translate3d(0, ${offset}px, 0)` }"
    class="ParallaxElement"
  >-->
    <slot />
  </v-img>
</template>

<script>
export default {
  name: 'ParallaxElement',
  inject: ['parallax'],
  props: {
    factor: {
      default: 0.25,
      type: Number
    }
  },
  computed: {
    offset () {
      const { scrollFactor } = this.parallax
      // const speed = 0.5
      // const pageTop = window.scrollY
      // const newTop = (top - (pageTop * speed))
      return scrollFactor * (this.factor / 2) //  * height * this.factor
    }
  }
}
</script>
