<template>
  <div class="element_data" v-if="element_data">
    <component :is="element_data.link?'a':'span'" :href="element_data.link || ''"  target="_blank">
       

         <div v-if="view=='vertical'" style="display: inline-block; _background-color: red; text-align: center;">
            <img :src="element_data.img" :style="{ width: img_size }">
            <p style="margin-top:10px; margin-bottom:-2px;" :style="title__style" :style_="{ fontSize: title_size, fontFamily: title_fontFamily }">{{ element_data.title }}</p>
            <p v-if='!(subtitle_hidden=="true")' :style="{ fontSize: subtitle_size}">{{subtitle_hidden}} {{ element_data.subtitle }}</p>
         </div>

        <div v-if="view=='horizontal'" >
            <div class="container">
                <div class="fixed">
                    <div style="text-align: left">
                        <img :src="element_data.img" :style="{ width: img_size }">
                    </div>
                </div>
                <div class="flex-item">
                    <div style="text-align: left; margin-top: 4px;">
                        <p style="margin-left: 10px; margin-bottom: -3px;" :style="title__style" :style_="{ fontSize: title_size, fontFamily: title_fontFamily }">{{ element_data.title }}</p>
                        <p v-if='!(subtitle_hidden=="true")' style="margin-left: 10px;" :style="{ fontSize: subtitle_size }">{{ element_data.subtitle }}</p>
                    </div>
                </div>
            </div>
        </div>
    </component>
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
   
    .container{
        /* background-color: blue; */
        display: flex;
        
    }
    .fixed{
        /* width: 100px; */
    }
    .flex-item{
        flex-grow: 1;
    }
    a {
        /* margin: 0; */
        color: black;
        text-decoration:none;
    }
    h1 {
        /* margin: 0; */
        font-size: 50px;
        font-family: 'Courier New', Courier, monospace;
        color: black;
    }
    h2, a {
        /* margin: 0; */
        font-size: 30px;
        color: black;
    }
</style>

<script>
    import axios from 'axios'

    export default {
        name: 'rad_logo',
        props: {
            view: String,
            data: String,
            img_style: String,
            img_size: String,
            title_size: String,
            title_style: String,
            title_fontFamily: String,
            subtitle_hidden: String,
            subtitle_size: String,
            desc_size: String

        },
        computed: {
            img__style () {
                return this.img_style;
            },
            title__style () {
                return this.title_style;
            }
        },
        data () {
            return {
                element_data: null
            }
        },
        mounted () {
            axios
            .get('elements.json')
            .then((response) => {
                var data = response.data
                console.log('response.data:' + data)
                console.log('response:' + response.data[this.data])
                this.element_data = response.data[this.data];
            });
        }
    }
</script>


