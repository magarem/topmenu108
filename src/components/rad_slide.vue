<template>
    <carousel perPage=1 :navigationEnabled="true" :autoplay=true v-if="slide">
        <slide v-for="item in slide.list" :key="item">
            <img :src="item">
        </slide>
    </carousel>
</template>

<script>
    // YourComponent.vue
    // import { VueAgile } from 'vue-agile'
    import { Carousel, Slide } from 'vue-carousel';
    import axios from 'axios'

    export default { 
        name: 'rad_slide',
        props: {
            size: String
        },
        components: {
            //agile: VueAgile
            Carousel, Slide
        },
        data () {
            return {
                slide: null
            }
        },
        mounted () {
            axios
            .get('elements.json')
            .then((response) => {
                console.log('response:' + response.data.slide)
                this.slide = response.data.slide;
            });
        }
    }
</script>

<style scoped>
    img {
        max-width: 100%;
        max-height: 100%;
    }
    .slide {
        height: 500px;
    }
</style>
