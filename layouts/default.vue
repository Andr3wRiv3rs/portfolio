<template>
  <div id="main">
    <div :class="page === 'stuff' ? '':'off'"><stuff/></div>
    <div :class="page === 'gallery' ? '':'off'"><gallery/></div>
    <div :class="page === 'music' ? '':'off'"><music/></div>
    <div :class="page === 'social' ? '':'off'"><social/></div>

    <div id="nav">
      <button v-for="i in [
        'stuff',
        'gallery',
        'music',
        'social'
      ]" :key="i" :id="`button-${i}`" v-on:click="changePage(i)" :class="page===i ? 'active nav-button':'inactive nav-button'"></button>
    </div>
  </div>
</template>

<script>
  import Stuff from "~/components/stuff.vue"
  import Gallery from "~/components/gallery.vue"
  import Music from "~/components/music.vue"
  import Social from "~/components/social.vue"

  export default {
    data () {
      return {
        page: 'stuff'
      }
    },

    components: {
      Stuff,
      Gallery,
      Music,
      Social,
    },

    methods: {
      changePage(pageInput) {
        this.page = pageInput            
      }
    }
  }
</script>