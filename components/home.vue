<template>
    <div id="home">
        <div id="header">
            <h1>Andres Sweeney-Rios</h1>
            <h2>Fullstack Web Developer, Game Developer, and Digital Artist.</h2>
            <div id="links">
                <a href="https://twitter.com/Andr3wRiv3rs" target="_blank"><img src="/images/icons/twitter.svg"/></a
                ><a href="https://gamejolt.com/@AndrewRivers" target="_blank"><img src="/images/icons/gamejolt.svg"/></a
                ><br><a href="https://github.com/Andr3wRiv3rs" target="_blank"><img src="/images/icons/github.svg"/></a
                ><a href="https://soundcloud.com/andr3wriv3rs" target="_blank"><img src="/images/icons/soundcloud.svg"/></a>
                <div>
                    andrewarivers@gmail.com<br>
                    Poison Apple#9351
                </div>
            </div>
        </div>
        <div id="skills">
            <p v-for="i in skills" :key="i">{{i}}</p>
        </div>
        <div id="home-navbar-bg"></div>
    </div>
</template>
<script>
    export default {
        data () {
            return {
                skills: [
                    'HTML/CSS','JavaScript','Node.js','Vue.js','Nuxt.js','Stylus',
                    'SCSS','jQuery','Express','NGINX','Apache',
                    'PHP','WordPress','Electron','Phonegap',
                    'MongoDB','MySQL','discord.js',
                    'Unity','Godot','GameMaker: Studio','Phaser',
                    'Construct 2','GIMP','Inkscape','Hexels',
                    'Aseprite','MagicaVoxel','VoxelShop','Qubicle','Blender'
                ]
            }
        }
    }
</script>