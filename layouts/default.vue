<template>
  <div id="main">
    <div :class="page === 'home' ? '':'off'"><home/></div>
    <div :class="page === 'stuff' ? '':'off'"><stuff/></div>
    <div :class="page === 'gallery' ? '':'off'"><gallery/></div>
    <div :class="page === 'music' ? '':'off'"><music/></div>

    <div id="nav">
      <button v-for="i in [
        'home',
        'stuff',
        'gallery',
        'music'
      ]" :key="i" :id="`button-${i}`" v-on:click="changePage(i)" :class="page===i ? 'active nav-button':'inactive nav-button'"></button>
    </div>
  </div>
</template>

<script>
  import Stuff from "~/components/stuff.vue"
  import Gallery from "~/components/gallery.vue"
  import Music from "~/components/music.vue"
  import Home from "~/components/home.vue"

  export default {
    data () {
      return {
        page: 'home'
      }
    },

    components: {
      Home,
      Stuff,
      Gallery,
      Music
    },

    methods: {
      changePage(pageInput) {
        this.page = pageInput            
      }
    },

    mounted () {
      window.onkeydown = e => {
        if (e.keyCode > 48 && e.keyCode < 53) this.page = ['home','stuff','gallery','music'][e.keyCode - 49]
      }
    }
  }
</script>