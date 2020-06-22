 <template>
    <!-- Footer-->
    <footer v-if=footer class="footer text-center">
        <div class="container">
            <div class="row">
              
                <!-- Footer Location-->
                <div class="col-lg-4 mb-5 mb-lg-0" v-for="(item, index) in footer.list" :key="index">
                    <h4 class="text-uppercase mb-4">{{item.title}}</h4>
                    <p class="lead mb-0">{{item.body}}</p>
                </div>



                <!-- Footer Social Icons
                <div class="col-lg-4 mb-5 mb-lg-0">
                    <h4 class="text-uppercase mb-4">{{data.footer.socialmidia.heading}}</h4>
                    <a class="btn btn-outline-light btn-social mx-1" :href="data.footer.socialmidia.link.facebook"><i class="fab fa-fw fa-facebook-f"></i></a>
                    <a class="btn btn-outline-light btn-social mx-1" :href="data.footer.socialmidia.link.twitter"><i class="fab fa-fw fa-twitter"></i></a>
                    <a class="btn btn-outline-light btn-social mx-1" :href="data.footer.socialmidia.link.linkedin"><i class="fab fa-fw fa-linkedin-in"></i></a>
                </div> -->
                <!-- Footer About Text-->
                <!-- <div class="col-lg-4">
                    <h4 class="text-uppercase mb-4">{{data.footer.footerabout.heading}}</h4>
                    <p class="lead mb-0">{{data.footer.footerabout.txt}}</p>
                </div> --> 
            </div>
        </div>
    </footer>
</template>

<script>
    import axios from 'axios'

    export default {
        name: 'freelancer_footer',
        props: {
            data: String
        },
        data () {
            return {
                footer: null
            }
        },
        mounted () {
            axios
            .get('elements.json')
            .then((response) => {
                console.log('response:' + response.data[this.data])
                this.footer = response.data[this.data];
            });
        }
    }
</script>