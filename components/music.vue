<template>
    <div id="music">
        <div id="nowplaying">
            <div class="bg"><img :src="`/images/covers/${songs[index].n.replace('.mp3','.png')}`"/></div>
            <h2>{{songs[index].d}}</h2>
            <div id="np-button" :alt="songs[index].n" class="cover" :style="`background-image:url(/images/covers/${songs[index].n.replace('.mp3','.png')});`"></div>
            <p class="desc off" v-html="songs[index].desc"></p>

            <span id="np-bar-wrapper">
                <span class="load-bar" id="np-bar-bg"></span>
                <span class="load-bar" id="np-bar" :style="`width: ${bar};`"></span>
                <span class="load-bar" id="np-bar-pad"></span>
            </span>

            <div id="controls"> 
                <button v-on:click="prev()" :class="index === 0 ? 'disabled' : ''">&lt;</button>
                <button class="play" v-on:click="pause(); $forceUpdate()">{{ nowplaying.paused ? "►" : "❚❚"}}</button>
                <button v-on:click="next()" :class="index === songs.length-1 ? 'disabled' : ''">&gt;</button>
            </div>
        </div>
        <div id="playlist">
            <div v-for="(i,k) in songs" class="track" :key="i.n" v-on:click="play(k)">
                <div class="track-inner">
                    <button v-on:click=" $forceUpdate()" :style="`background-image:url(/images/covers/${i.n.replace('.mp3','.png')});`" class="play-button">{{ index === k ? nowplaying.paused ? "►" : "❚❚" : ""}}</button>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import {songs} from "~/components/songs.js"
    export default {
        data () { 
            return {
                songs,
                nowplaying: {paused:true,init:true},
                index: 0,
                bar: 0
            }
        },

        methods: {
            play (index) {
                if (this.index === index && !this.nowplaying.init) {
                    this.pause();
                    this.$forceUpdate();
                } else {
                    this.index = index;

                    if (this.nowplaying.init) {
                        this.nowplaying = document.createElement('AUDIO');
                        this.nowplaying.onended = () => {
                            if (index < this.songs.length) this.play(index+1);
                            else index = 0
                        }
                    }

                    const bar = setInterval(() => this.bar = 100 / (this.nowplaying.duration / this.nowplaying.currentTime) + '%', 10);

                    this.nowplaying.src = '/music/'+songs[index].n;
                    this.nowplaying.play();
                }
            },

            pause () {
                if (!this.nowplaying.init) {
                    if (this.nowplaying.paused) this.nowplaying.play(index)
                    else this.nowplaying.pause()
                } else {
                    this.play(0)
                }
            },

            next () {
                this.play(this.index+1)
            },

            prev () {
                this.play(this.index-1)
            }
        },

        mounted () {
            const $ = e => document.querySelector(e);
            const npBar = $('#np-bar-pad');
            npBar.onclick = e => {
                this.nowplaying.currentTime = this.nowplaying.duration / ($('#np-bar-pad').clientWidth / (e.clientX - $('#np-bar-pad').offsetLeft));
            };
        }
    }
</script>