<template>
  <div class="element_data" v-if="element_data">
    <component :is="element_data.link?'a':'span'" :href="element_data.link || ''"  target="_blank">
       
        <div v-if="type=='default'" >
            <div class="container">
                <div class="fixed">
                    <div style="text-align: center">
                        <img class=img_wrapped style="margin-bottom: 30px;" :src="element_data.img" :style="style">
                        <div style="text-align: left">
                            <p style="margin-left: 10px; margin-bottom: -3px;" :style="{ fontSize: title_size, fontFamily: title_fontFamily }">{{ element_data.title }}</p>
                            <p style="margin-left: 10px; " :style="{ fontSize: subtitle_size }">{{ element_data.subtitle }}</p>
                            <p style="margin-left: 10px; " :style="{ fontSize: desc_size }">{{ element_data.desc }}</p>
                        </div>
                    </div>
                </div>
            </div>
        </div>
        <div v-if="type=='default_left_wrapper'" >
            <div class="container">
                <div class="fixed">
                    <div style="text-align: left">
                        <img class=img_wrapped_left :src="element_data.img" :style="style">
                        <p style="margin-left: 10px; margin-bottom: -3px;" :style="{ fontSize: title_size, fontFamily: title_fontFamily }">{{ element_data.title }}</p>
                        <p style="margin-left: 10px; " :style="{ fontSize: subtitle_size }">{{ element_data.subtitle }}</p>
                        <p style="margin-left: 10px; " :style="{ fontSize: desc_size }">{{ element_data.desc }}</p>
                    </div>
                </div>
            </div>
        </div>
        <div v-if="type=='default_right_wrapper'" >
            <div class="container">
                <div class="fixed">
                    <div style="text-align: right">
                        <img class=img_wrapped_right :src="element_data.img" :style="style">
                        <p style="margin-left: 10px; margin-bottom: -3px;" :style="{ fontSize: title_size, fontFamily: title_fontFamily }">{{ element_data.title }}</p>
                        <p style="margin-left: 10px; " :style="{ fontSize: subtitle_size }">{{ element_data.subtitle }}</p>
                        <p style="margin-left: 10px; " :style="{ fontSize: desc_size }">{{ element_data.desc }}</p>
                    </div>
                </div>
            </div>
        </div>

         <div v-if="type=='logo_vertical'" style="background-color: red_; text-align: center;">
            <img :src="element_data.img" :style="{ width: img_size }">
            <p style="margin-top:10px; margin-bottom:-2px;" :style="{ fontSize: title_size, fontFamily: title_fontFamily }">{{ element_data.title }}</p>
            <p :style="{ fontSize: subtitle_size}">{{ element_data.subtitle }}</p>
            <p :style="{ fontSize: desc_size }">{{ element_data.desc }}</p>
         </div>

        <div v-if="type=='logo_horizontal'" >
            <div class="container">
                <div class="fixed">
                    <div style="text-align: left">
                        <img :src="element_data.img" :style="{ width: img_size }">
                    </div>
                </div>
                <div class="flex-item">
                    <div style="text-align: left; margin-top: 4px;">
                        <p style="margin-left: 10px; margin-bottom: -3px;" :style="{ fontSize: title_size, fontFamily: title_fontFamily }">{{ element_data.title }}</p>
                        <p style="margin-left: 10px; " :style="{ fontSize: subtitle_size }">{{ element_data.subtitle }}</p>
                        <p style="margin-left: 10px; " :style="{ fontSize: desc_size }">{{ element_data.desc }}</p>
                    </div>
                </div>
            </div>
        </div>


        <div v-if="type=='card'">
            <b-card
                :title="this.element_data.title"
                :img-src="this.element_data.img"
                img-alt="Image"
                img-top
                tag="article"
                :style="style"
                class="mb-2"
            >
                <b-card-text>
                    {{this.element_data.desc}}
                </b-card-text>

                <!-- <b-button href="#" variant="primary">Go somewhere</b-button> -->
            </b-card>
        </div>

    
    </component>
  </div>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    /* img {border: 10px solid rgb(80, 83, 29)} */
    .img_wrapped_left {
        float: left;
        margin: 10px 20px 10px 0;
    }
    .img_wrapped_right {
        float: right;
        margin: 10px 0px 10px 15px;
    }

    .p_wraper {
        text-align: justify;
        text-indent: 2em;
    }
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
        name: 'rad_default',
        props: {
            type: String,
            view: String,
            data: String,
            img_style: String,
            img_size: String,
            title_size: String,
            title_fontFamily: String,
            subtitle_size: String,
            desc_size: String

        },
        computed: {
            style () {
                return this.img_style;
            }
        },
        data () {
            return {
                element_data: null
            }
        },
        mounted () {
            console.log("this.data_:", this.data);
            axios
            .get('elements.json')
            .then((response) => {
                var data = response.data
                console.log('response.data:' + data)
                console.log('response.data.logo:' + data.logo)
                console.log('response:' + response.data[this.data])
                this.element_data = response.data[this.data];
            });
        }
    }
</script>


