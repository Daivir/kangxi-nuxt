<template>
  <v-app v-scroll="handleScroll" v-resize="handleResize">
    <v-navigation-drawer
      v-model="drawer"
      app
    >
      <v-list-item>
        <v-list-item-content>
          <v-list-item-title class="nav-title">
            Application
          </v-list-item-title>
          <v-list-item-subtitle>
            subtext
          </v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>
      <v-divider />
      <v-list
        dense
        nav
      >
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.route"
          link
        >
          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      app
      elevation="0"
      hide-on-scroll
    >
      <v-app-bar-nav-icon @click="drawer = !drawer" />
      <div class="flex-grow-1" />
      <v-btn icon>
        <v-icon>{{ icon.search }}</v-icon>
      </v-btn>
      <v-btn icon>
        <v-icon>{{ icon.more }}</v-icon>
      </v-btn>
    </v-app-bar>
    <v-content ref="content">
      <v-container>
        <div ref="carousel">
          <v-carousel
            v-model="handleResize"
            :height="carouselWidth / (16/9)"
            continuous
            cycle
            hide-delimiters
            show-arrows-on-hover
          >
            <v-carousel-item v-for="n in 3" :key="n">
              <v-img
                :aspect-ratio="16/9"
                :src="'https://picsum.photos/1280/720?random=' + n"
                :lazy-src="'https://picsum.photos/16/9?random=' + n"
              >
                <template v-slot:placeholder>
                  <v-row
                    class="fill-height ma-0"
                    align="center"
                    justify="center"
                  >
                    <v-progress-circular indeterminate color="grey lighten-5"></v-progress-circular>
                  </v-row>
                </template>
              </v-img>
            </v-carousel-item>
          </v-carousel>
        </div>
        {{ carouselWidth }}
        <nuxt />
        <div style="height:100vh;" />
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    offsetTop: 0,
    carouselWidth: 0,
    drawer: true,
    image: 'https://picsum.photos/1280/720',
    title: 'galerie kangxi',
    icon: {
      menu: 'mdi-menu',
      search: 'mdi-magnify',
      more: 'mdi-dots-vertical'
    },
    items: [
      { title: 'Accueil', route: { path: '/' } },
      { title: 'Nouveautés', route: { path: '/latest' } }
    ]
  }),
  computed: {},
  created () {},
  mounted () {
    this.handleScroll()
    this.$nextTick(() => {
      this.handleResize()
    })
  },
  updated () {},
  destroyed () {},
  methods: {
    handleResize () {
      this.carouselWidth = this.$refs.carousel.clientWidth
      // const rect = e.target.getBoundingClientRect()
      // this.dimensions = {} // x: rect.width, y: rect.height }
    },
    handleScroll () {
      this.offsetTop = window.scrollY
    }
  }
}
</script>

<style lang="scss">
</style>
