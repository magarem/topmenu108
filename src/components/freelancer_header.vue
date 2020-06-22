<template>
     <!-- Masthead-->
        <header v-if=data class="masthead bg-primary text-white text-center">
            <div class="container d-flex align-items-center flex-column">
                <div class="image-cropper mb-5">
                  <img :src="data.img" alt="avatar" class="profile-pic">
                </div>
                <h1 class="masthead-heading text-uppercase_ mb-0">{{data.title}}</h1>
                <!-- Icon Divider-->
                <div class="divider-custom divider-light">
                    <div class="divider-custom-line"></div>
                    <div class="divider-custom-icon"><i class="fas fa-star"></i></div>
                    <div class="divider-custom-line"></div>
                </div>
                <!-- Masthead Subheading-->
                <p class="masthead-subheading font-weight-light mb-0">{{data.subtitle}}</p>
            </div>
        </header>
</template>
<style scoped>
  @import url('https://fonts.googleapis.com/css?family=Varela+Round');
  h1 {
    font-family: 'Varela Round', Helvetica, Arial, sans-serif;
  }
</style>
<script>
    import axios from 'axios'
    export default {
        props: {
            source: String
        },
        data () {
            return {
                data: null
            }
        },
        mounted () {
            axios
            .get('elements.json')
            .then((response) => {
                console.log('response:' + response.data[this.source])
                this.data = response.data[this.source];
            });
        }
    }
</script>