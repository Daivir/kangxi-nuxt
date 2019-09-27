<template>
  <v-app>
    <header class="white pt-4" :style="style.header">
      <nav class="d-flex align-center px-2" :style="style.nav">
        <v-btn class="mr-2" icon>
          <v-icon>{{ icon.menu }}</v-icon>
        </v-btn>
        <div class="nav-title">
          {{ title }}
        </div>
        <div class="flex-grow-1" />
        <v-btn icon>
          <v-icon>{{ icon.search }}</v-icon>
        </v-btn>
        <v-btn icon>
          <v-icon>{{ icon.more }}</v-icon>
        </v-btn>
      </nav>
    </header>
    <v-content :style="style.content">
      <div v-scroll="onScroll" style="overflow: hidden;">
        <v-img
          src="https://picsum.photos/1280/720"
          :aspect-ratio="16/9"
          :style="{ transform: `translate3d(0, ${offset}px, 0)`, opacity: 1 - (offset / 100 * offset) / 100 }"
        >
          <div class="d-flex align-center justify-center fill-height nav-title" style="font-size:24px;">
            {{ title }}
          </div>
        </v-img>
      </div>
      <v-container>
        <div style="background-color: #fff;height:100vh;">
          {{ offset }}
        </div>
      </v-container>
    </v-content>
    <!--<div class="parallax" :style="style.content">
      <div class="parallax__layer&#45;&#45;back">
        <v-img class="parallax__img" src="https://picsum.photos/1280/720" :aspect-ratio="16/9" />
      </div>
      <v-container class="parallax__layer&#45;&#45;base">
        <nuxt />
        <div style="height:200vh;" />
      </v-container>
    </div>-->
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      offset: 0,
      dark: true,
      title: 'galerie kangxi',
      icon: {
        menu: 'mdi-menu',
        search: 'mdi-magnify',
        more: 'mdi-dots-vertical'
      }
    }
  },
  computed: {
    style () {
      return {
        header: { position: 'fixed', width: '100%', zIndex: '1' },
        nav: { height: '56px' },
        content: { marginTop: (56 + 16) + 'px' }
      }
    }
  },
  methods: {
    onScroll () {
      // if (window.scrollY >= 1) {
      //   window.scrollY = 202.5
      // }
      // this.offset = ((window.scrollY - this.$el.getBoundingClientRect().top) / this.$el.getBoundingClientRect().height)
      this.offset = window.scrollY * 0.5
    }
  }
}
</script>

<style lang="scss">
  .App__example-single-element {
  }
</style>
