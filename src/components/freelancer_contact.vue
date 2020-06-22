<template>
    <!-- Contact Section-->
    <section v-if=contact class="page-section" id="contact">
        <div class="container">
            <!-- Contact Section Heading-->
            <h2 class="page-section-heading text-center text-uppercase text-secondary mb-0">{{contact.title}}</h2>
            <!-- Icon Divider-->
            <div class="divider-custom">
                <div class="divider-custom-line"></div>
                <div class="divider-custom-icon"><i class="fas fa-star"></i></div>
                <div class="divider-custom-line"></div>
            </div>
            <!-- Contact Section Form-->
            <div class="row">
                <div class="col-lg-8 mx-auto">
                    <form id="contactForm" name="sentMessage" novalidate="novalidate">
                        <div class="control-group" v-for="(item, index) in contact.list" :key="index">
                            <div v-if="item.type !== 'submit'" class="form-group floating-label-form-group controls mb-0 pb-2">
                                <label>{{ item.name }}</label><input class="form-control" :id="item.name" type="text" :placeholder="item.name" required="required" :data-validation-required-message="item.name" />
                                <p class="help-block text-danger"></p>
                            </div>
                            <div v-else>
                                <br />
                                <div id="success"></div>
                                <div class="form-group"><button class="btn btn-primary btn-xl" id="sendMessageButton" type="submit">{{item.name}}</button></div>
                            </div>
                        </div>

                    </form>
                </div>
            </div>
        </div>
    </section>
</template>
<script>
    import axios from 'axios'

    export default {
        name: 'freelancer_contact',
        props: {
            data: String
        },
        data () {
            return {
                contact: null
            }
        },
        mounted () {
            axios
            .get('elements.json')
            .then((response) => {
                console.log('response:' + response.data[this.data])
                this.contact = response.data[this.data];
            });
        }
    }
</script>