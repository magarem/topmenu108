<template>
  <div v-if=data>
    <!-- Portfolio Section-->
    <section class="page-section portfolio" id="portfolio">
        <div class="container">
            <!-- Portfolio Section Heading-->
            <h2 class="page-section-heading text-center text-uppercase text-secondary mb-0">{{data.title}}</h2>
            <!-- Icon Divider-->
            <div class="divider-custom">
                <div class="divider-custom-line"></div>
                <div class="divider-custom-icon"><i class="fas fa-star"></i></div>
                <div class="divider-custom-line"></div>
            </div>
            <!-- Portfolio Grid Items-->
            <div class="row">
                
            <div class="col-md-6 col-lg-4 mb-5" v-for="(item, index) in data.list" :key="index">
                <b-card
                    :title="item.title"
                    :img-src="item.img"
                    img-alt="Image"
                    img-top
                    tag="article"
                    class="mb-2">
                    <b-card-text>
                        
                        <div class="row mt-3">
                            <div class="col-sm" >
                                <span class=price>R$ {{item.price}}</span>
                            </div>
                           <div class="col-sm">
                                <div class="quantity">
                                    <b-input-group>
                                    <b-input-group-prepend>
                                        <b-btn variant="info" @click="decrement(item)">-</b-btn>
                                    </b-input-group-prepend>

                                    <b-form-input type="number" min="0.00" :value="item.qnt"></b-form-input>

                                    <b-input-group-append>
                                        <b-btn variant="info" @click="increment(item)">+</b-btn>
                                    </b-input-group-append>
                                    </b-input-group>
                                </div>
                            </div>
                        </div>
                    </b-card-text>
                <!-- <b-button href="#" variant="primary">Go somewhere</b-button> -->
                    
                </b-card>
            </div>

                
                <!-- Portfolio Item -->
                <!-- <div  class="col-md-6 col-lg-4 mb-5" v-for="(item, index) in data.list" :key="index">
                    <div class="portfolio-item mx-auto" data-toggle="modal" :data-target="'#portfolioModal' + source + index">
                        <div class="portfolio-item-caption d-flex align-items-center justify-content-center h-100 w-100">
                            <div class="portfolio-item-caption-content text-center text-white"><i class="fas fa-plus fa-3x"></i></div>
                        </div>
                        <img style="width: 100%; height: 240px; object-fit: cover;" :src="item.img" alt="" />
                        {{item.title}}
                    </div>
                </div> -->


            </div>
        </div>
    </section>
<!-- Portfolio Modals--><!-- Portfolio Modal 1-->
        <div class="portfolio-modal modal fade" v-for="(item, index) in data.list" :key="index" :id="'portfolioModal'+ source + index" tabindex="-1" role="dialog" aria-labelledby="portfolioModal1Label" aria-hidden="true">
            <div class="modal-dialog modal-xl" role="document">
                <div class="modal-content">
                    <button class="close" type="button" data-dismiss="modal" aria-label="Close">
                        <span aria-hidden="true"><i class="fas fa-times"></i></span>
                    </button>
                    <div class="modal-body text-center">
                        <div class="container">
                            <div class="row justify-content-center">
                                <div class="col-lg-8">
                                    <!-- Portfolio Modal - Title-->
                                    <h2 class="portfolio-modal-title text-secondary text-uppercase mb-0">{{item.title}}</h2>
                                    <!-- Icon Divider-->
                                    <div class="divider-custom">
                                        <div class="divider-custom-line"></div>
                                        <div class="divider-custom-icon"><i class="fas fa-star"></i></div>
                                        <div class="divider-custom-line"></div>
                                    </div>
                                    <!-- Portfolio Modal - Image--><img class="img-fluid rounded mb-5" :src="item.img" alt="" /><!-- Portfolio Modal - Text-->
                                    <p class="mb-5">{{item.txt}}</p>
                                    <button class="btn btn-primary" href="#" data-dismiss="modal"><i class="fas fa-times fa-fw"></i>Fechar</button>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<style scoped>
    .price {
        color: green;
        font-size: 30px;
    }
</style>

<script>
    import axios from 'axios'

    export default {
        name: 'freelancer_portfolio',
        props: {
            source: String
        },
        data () {
            return {
                data: null,
                quantity: []
            }
        },
        methods: {
            addToCart(item) {
                this.$emit('update-cart', item)
            },
            upd() {
                this.$emit('upd', this.data.list)
            },
            increment(item) {
                console.log(item);
                item.qnt++;
                // this.addToCart(item)
                this.upd()
                // this.quantity[index]++;
            },
            decrement(item) {
                console.log(item);
                item.qnt--;
                // this.addToCart(item)
                this.upd()
                
                // if (this.quantity === 1) {
                //     alert("Negative quantity not allowed");
                //     } else {
                //         this.quantity[index]--;
                // }
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