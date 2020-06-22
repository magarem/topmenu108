<template>
    <ul v-if=element_data :class="ul_class">
        <li :class="ul_li_class" v-for="(item, idx) in element_data.list" :key="idx">
            <a :class="ul_li_a_class" :href="item.target">{{item.label}}</a>
        </li>
    </ul>
</template>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    #nav{
        border:1px solid #ccc;
        border-width:1px 0;
        list-style:none;
        margin:0;
        padding:0;
        text-align:center;
    }
    #nav li{
        display:inline;
    }
    #nav a{
        display:inline-block;
        padding:10px;
    }
    a{
        color:#c00;
        text-decoration:none;
        font-weight:bold;
    }
    a:hover{
        text-decoration:underline;
    }
</style>

<script>
    import axios from 'axios'

    export default {
        name: 'rad_menu',
        props: {
            ul_class: String,
            ul_li_class: String,
            ul_li_a_class: String,
            data: String,
            size: String
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
                console.log(this.data)
                console.log('response:' + response.data[this.data].list)
                this.element_data = response.data[this.data];
            });
        }
    }
</script>


