 <template>
    <!-- About Section-->
    <section v-if=about class="page-section bg-primary text-white mb-0" id="about">
        <div class="container">
            <!-- About Section Heading-->
            <h2 class="page-section-heading text-center text-uppercase text-white">{{about.title}}</h2>
            <!-- Icon Divider-->
            <div class="divider-custom divider-light">
                <div class="divider-custom-line"></div>
                <div class="divider-custom-icon"><i class="fas fa-star"></i></div>
                <div class="divider-custom-line"></div>
            </div>
            <!-- About Section Content-->
            <div class="row">
                <div class="col-lg-4 ml-auto"><p class="lead">{{about.body}}</p></div>
                <div class="col-lg-4 mr-auto"><p class="lead">{{about.body}}</p></div>
            </div>
            <!-- About Section Button-->
            <!-- <div class="text-center mt-4">
                <a class="btn btn-xl btn-outline-light" href="https://startbootstrap.com/themes/freelancer/"><i class="fas fa-download mr-2"></i>Free Download!</a>
            </div> -->
        </div>
    </section>
</template>
<script>
    import axios from 'axios'

    export default {
        name: 'freelancer_about',
        props: {
            data: String
        },
        data () {
            return {
                about: null
            }
        },
        mounted () {
            axios
            .get('elements.json')
            .then((response) => {
                console.log('response:' + response.data[this.data])
                this.about = response.data[this.data];
            });
        }
    }
</script>