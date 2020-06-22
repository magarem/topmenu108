<template>
    <!-- Copyright Section-->
    <section v-if=data class="copyright py-4 text-center text-white">
        <div>
            <b-button @click="update" >Update</b-button>
            <b-button @click="alert()" v-b-modal.modal-lg variant="primary">lg modal</b-button>
            <b-modal id="modal-lg" size="lg" title="Large Modal">
                <table class="table">
  <thead>
      {{data.portfolio.list[0].qnt}}
    <tr>
      <th scope="col">#</th>
      <th scope="col">First</th>
      <th scope="col">Last</th>
      <th scope="col">Handle</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">1</th>
      <td>Mark</td>
      <td>Otto</td>
      <td>@mdo</td>
    </tr>
    <tr>
      <th scope="row">2</th>
      <td>Jacob</td>
      <td>Thornton</td>
      <td>@fat</td>
    </tr>
    <tr>
      <th scope="row">3</th>
      <td>Larry</td>
      <td>the Bird</td>
      <td>@twitter</td>
    </tr>
  </tbody>
</table>
            </b-modal>
        </div>
        <!-- <div class="container"><small>Copyright © <a :href='data.link'>{{data.title}}</a></small></div> -->
    </section>
</template>
<script>
    import axios from 'axios'

    export default {
        name: 'freelancer_copyright',
        props: {
            source: String
        },
        data () {
            return {
                data: null
            }
        },
        methods:{
            update (){
                alert()
                 axios
                .get('elements.json')
                .then((response) => {
                    // console.log('response:' + response.data[this.source])
                    // this.data = response.data[this.source];
                    console.log('response:' + response.data)
                    this.data = response.data;
                });
            }
        },
        mounted () {
            axios
            .get('elements.json')
            .then((response) => {
                // console.log('response:' + response.data[this.source])
                // this.data = response.data[this.source];
                console.log('response:' + response.data)
                this.data = response.data;
            });
        }
    }
</script>