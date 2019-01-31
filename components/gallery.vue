<template>
    <div id="gallery">
        <div id="gallery-background" :style="`background-image:url(/images/gallery/${current}.png);`"></div>
        <div id="gallery-inner">
            <div id="gallery-preview-wrapper">
                <div id="gallery-preview">
                    <div  class="preview-thumb" v-for="(i,k) in images" :alt="i" :class="index === k ? 'active':''" :key="i" v-on:click="selectImage(i,k)"  :style="`background-image:url(/images/gallery/${i}.png);`"></div>
                </div>
            </div>
            <div id="gallery-image">
                <!-- <img id="image-current" :src="`/images/gallery/${current}.png`"> -->
                <div id="gallery-image-inner" :style="`background-image:url(/images/gallery/${current}.png);`"></div>
            </div>
            <div id="gallery-controls">
                <div class="left" v-on:click="next()">
                    &lt;
                </div>
                <div class="right" v-on:click="prev()">
                    &gt;
                </div>
            </div>
            <h1 id="index">{{index+1}}</h1>
        </div>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                images: [
                    "0-AppleZkkov",
                    "0-ArcticApple",
                    "0-RadApple",
                    "0-YinApple",
                    "adamant",
                    "daily2",
                    "dren",
                    "gameboy_jellyfish",
                    "heart",
                    "pink_cityscape_large",
                    "pink_space",
                    "polygon",
                    "triskele",
                    "tulip_large",
                    "unknown-14",
                    "unknown-46",
                    "waterfall"
                ],
                current: '0-AppleZkkov',
                index: 0
            }
        },

        methods: {
            selectImage (i,index) {
                this.current = i;
                this.index = index;

                const $ = e => document.querySelector(e);
                const preview = $('#gallery-preview');
                const thumb = preview.children[index];
                const wrapper = $('#gallery-preview-wrapper');

                if (index>2) preview.style.marginLeft = (thumb.clientWidth * index - (thumb.clientWidth * 1.5)) * -1 + 'px';
                else preview.style.marginLeft = 0;
                
                if (parseInt(preview.style.marginLeft) - (thumb.clientWidth/2) <= (preview.clientWidth - wrapper.clientWidth)*-1) 
                    preview.style.marginLeft = (preview.clientWidth - wrapper.clientWidth )*-1 + 'px'
            }
        }
    }
</script>
