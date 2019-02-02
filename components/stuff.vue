<template>
    <div id="stuff">
        <div id="stuff-inner" :style="`width: ${entries.length*100}vw; margin-left: ${left}vw;`">
            <div class="project" :style="`background-image:url(/images/stuff/${i.bg}.png); ${i.left ? 'background-position: left center;':''}`" v-for="i in entries" :key="i.title">
                <div class="info">
                    <h2 class="title">{{i.title}}</h2>
                    <p class="desc">{{i.desc}}</p>
                    <div class="handles">
                        <a v-for="h in i.handles" :key="h" :href="`https://twitter.com/`+h" target="_blank">@{{h}}</a>
                        <a v-for="h in i.gj_handles" :key="h" :href="`https://gamejolt.com/@`+h" target="_blank">@{{h}}</a>
                        <a v-for="h in i.ig_handles" :key="h" :href="`https://www.instagram.com/`+h" target="_blank">@{{h}}</a>
                    </div>
                    <div class="links"><a v-for="l in i.links" target="_blank" :key="l.type" :href="l.url" :style="`background-image:url(/images/icons/${l.type}.png);`"></a></div>
                </div>
            </div>

            <div id="bubbles">
                <span v-for="(i,k) in entries" :key="i.name" v-on:click="slide(k,true)" :class="index === k ? 'active' : ''"></span>
            </div>

            <div id="mobile-bubbles">
                <span v-for="(i,k) in entries" :style="`width:${60/entries.length}vw; height:${60/entries.length}vw;`" :key="i.name" v-on:click="slide(k,true)" :class="index === k ? 'active' : ''"></span>
            </div>
        </div>
    </div>
</template>
<script>
    import {entries} from "~/components/entries.js"

    export default { 
        data () {
            return {
                entries,
                left: 0,
                index: 0,
                clicked: false
            }
        },

        methods: {
            slide (key,clicked) {
                if (key<0) key = 0;
                if (key===entries.length) key = entries.length-1;
                this.left = -100 * key;
                this.index = key;
                if (clicked) this.clicked = true;
            }
        },

        mounted () {
            const autoSlide = setInterval(() => {
                if (!this.clicked) {
                    this.slide(this.index+1, false);
                    if (this.index === this.entries.length) this.slide(0, false);
                } else clearInterval(autoSlide);
            }, 10000);

            const stuff = document.getElementById('stuff');

            stuff.ontouchstart = touchstart => {
                stuff.ontouchmove = touchmove => {
                    const swipe = touchstart.touches[0].clientX - touchmove.touches[0].clientX;

                    if (swipe < -50) {
                        this.slide(this.index-1,true);
                        stuff.ontouchmove = () => {};
                    }

                    if (swipe > 50) {
                        this.slide(this.index+1,true);
                        stuff.ontouchmove = () => {};
                    }
                }
                stuff.ontouchend = () => {stuff.ontouchmove = () => {}}
            }
        }
    }
</script>
