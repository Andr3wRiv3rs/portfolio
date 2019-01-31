<template>
    <div id="music">
        <div id="nowplaying">
            <button id="np-button" :alt="songs[index].n" class="play-button" :style="`background-image:url(/images/covers/${songs[index].n.replace('.mp3','.png')});`"> {{ nowplaying.paused ? "►" : "❚❚"}}</button>
            <div class="np-inner-wrapper">
                <h2>{{songs[index].d}}</h2>
                <p class="desc" v-html="songs[index].desc"></p>
                <span class="load-bar" id="np-bar-bg"></span>
                <span class="load-bar" id="np-bar"></span>
                <span class="load-bar" id="np-bar-pad"></span>
            </div>
        </div>
        <div id="playlist">
            <div v-for="(i,k) in songs" class="track" :key="i.n" v-on:click="play(k)" >
                <div class="track-inner">
                    <button :style="`background-image:url(/images/covers/${i.n.replace('.mp3','.png')});`" class="play-button">
                        {{ true ? "►" : "❚❚"}}
                    </button>
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
                index: 0
            }
        },

        methods: {
            play (index) {
                this.index = index;

                if (this.nowplaying.init) {
                    this.nowplaying = document.createElement('AUDIO');
                    this.nowplaying.onended = () => {
                        index++;
                        if (index < this.songs.length) this.play(index);
                        else index = 0
                    }
                }

                this.nowplaying.src = '/music/'+songs[index].n;
                this.nowplaying.play();
            }
        }
    }
</script>