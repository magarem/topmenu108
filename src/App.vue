<template>
  <div id="app">
    <freelancer_navbar />
    <!-- <freelancer_header source=header /> -->
    <freelancer_portfolio source=portfolio @update-cart="updateCart" @upd="upd"/>
    <!-- <freelancer_about data=about /> -->
    <!-- <freelancer_portfolio source=portfolio2 /> -->
    <!-- <freelancer_about data=about2 /> -->
    <!-- <freelancer_contact data=contact /> -->
    <!-- <freelancer_footer data=footer /> -->
    
    
    <div class="fixed-bottom">
        <!-- <freelancer_copyright source=copyright /> -->
        <!-- Copyright Section-->
      <section  class="copyright py-4 text-center text-white">
          <div>
              <b-button class="mt-0"  v-b-modal.modal-lg  variant="primary">Continuar</b-button>
              <b-modal id="modal-lg" centered size="lg" title="" hide-footer body-class="pt-0">
                 
                   <rad_logo 
                data="logo" 
                view="horizontal"
                img_size = "50px"
                title_style = "color: black; font-size: 20px; font-family: 'Varela Round', Helvetica, Arial, sans-serif;"
                subtitle_hidden = true
                subtitle_size = "17px"
                desc_size = "11px"/><br>
                
                        <h3>Resumo do pedido</h3>
                      
                  <table class="table">
                    
                    <thead>
                      
                      <tr>
                        <th scope="col">#</th>
                        <th scope="col">Produto</th>
                        <th scope="col">Valor</th>
                        <th scope="col">Qtd.</th>
                        <!-- <th scope="col">Sub-total</th> -->
                      </tr>
                    </thead>
                    <tbody>
                      <tr v-for="(item, index) in sortedCart" :key="index">
                        <th scope="row">{{index + 1}}</th>
                        <td>{{item.title}}</td>
                        <td>R$ {{formatPrice(parseFloat(item.price))}}</td>
                        <td>{{item.qnt}}</td>
                        <!-- <td>{{parseInt(item.qnt) * parseInt(item.price)}}</td> -->
                      </tr>
                      <tr>
                        <td colspan=4>
                           Observações sobre o pedido:
                          <b-form-textarea
                            id="textarea"
                            v-model="text"
                            placeholder="Digite aqui..."
                            rows="3"
                            max-rows="6"></b-form-textarea>
                        </td>
                      </tr>
                      

                     <tr>
                        <th scope="row"></th>
                        <td></td>
                        <!-- <td></td> -->
                        <td align=right class=modal_cart_total_field>Subtotal:<br>R$ {{formatPrice(total)}}</td>
                        <td class=modal_cart_total_value>Taxa de entrega<br>Consulte</td>
                      </tr>
                      <tr>
                        <td colspan="4">
                          <h3>Informações para entrega</h3>
                        </td>
                      </tr>
                      <tr>
                        <td colspan="2"><b-form-input placeholder="Celular"></b-form-input></td>
                        <td colspan="2"><b-form-input placeholder="Nome"></b-form-input></td>
                      </tr>
                    </tbody>
                  </table>
                  <div>
                    <b-tabs content-class="mt-3" align="center">
                      <b-tab title="Entrega" active>
                          <div class="form-group row" style="box-sizing: border-box; padding: 0px;">
                            <div class="col-8" style="padding: 0 0 0 22px; box-sizing: border-box;">
                              <input type="text" class="form-control" placeholder="Endereço">
                            </div>
                            <div class="col-4" style="padding: 0 22px 0 2px;">
                              <input type="text" class="form-control"  placeholder="Número">
                            </div>
                          </div>
                          <div class="row">
                            <div class="col-5" style="padding: 0 5px 0 22px;">
                              <input type="text" class="form-control"  placeholder="Complemento">
                            </div>
                            <div class="col-3" style="padding: 0 0 0 0;">
                              <b-form-input  placeholder="Bairro"></b-form-input>
                            </div>
                            <div class="col-4" style="padding: 0 22px 0 5px;">
                              <b-form-input  placeholder="Cep"></b-form-input>
                            </div>
                          </div>
                          <div class="row mt-3">
                            <div class="col-12">
                              <b-form-input placeholder="Ponto de Referência"></b-form-input>
                            </div>
                          </div>
                      </b-tab>
                      <b-tab title="Retirar no local"><p>Retirar no local</p></b-tab>
                    </b-tabs><br>
                    <h3>Forma de pagamento</h3>
                    <b-tabs content-class="mt-3" align="center">
                      <b-tab title="Dinheiro" active>
                        Troco para:
                        <b-form-input placeholder="Ex: 100,00"></b-form-input>
                        <b-form-checkbox
                          id="checkbox-1"
                          v-model="status"
                          name="checkbox-1"
                          value="accepted"
                          unchecked-value="not_accepted"
                        >
                          Não preciso de troco
                        </b-form-checkbox>
                      </b-tab>
                      <b-tab title="Trazer maquininha" active>
                        <select class="custom-select mr-sm-2" id="inlineFormCustomSelect">
                          <option selected>Choose...</option>
                          <option value="1">Mastercard</option>
                          <option value="2">Visa</option>
                          <option value="3">Amercican Express</option>
                        </select>
                      </b-tab>
                    </b-tabs>

                  </div><br><br>
                  <h2>Confirme o pedido clicando no botão abaixo</h2>
                  <div class="col text-center"><Br/>
                    <b-button @click="sendOrder(sortedCart)" class="mt-3 btn-success" block >Enviar pedido</b-button>
                    
                    <b-button class="mt-3" block @click="$bvModal.hide('modal-lg')">Voltar</b-button>
                  </div>
              </b-modal>
          </div>
          <!-- <div class="container"><small>Copyright © <a :href='data.link'>{{data.title}}</a></small></div> -->
      </section>
    </div>
  </div>
</template>
<style scoped>
  .pp {
    padding-top: 0px;
  }
  h1, h2, h3, button{
    text-align: center;
  }
  table {
    font-size: 14px;
  }
  .modal_cart_total_field{
    font-size: 15px;
    color: rgb(7, 7, 7);
  }
  .modal_cart_total_value{
    font-size: 15px;
    color: green;
  }
</style>

<script>
  import freelancer_navbar from './components/freelancer_navbar.vue'
  // import freelancer_header from './components/freelancer_header.vue'
  import freelancer_portfolio from './components/freelancer_portfolio.vue'
  // import freelancer_about from './components/freelancer_about.vue'
  // import freelancer_contact from './components/freelancer_contact.vue'
  // import freelancer_footer from './components/freelancer_footer.vue'
  // import freelancer_copyright from './components/freelancer_copyright.vue'
  import rad_logo from './components/rad_logo.vue'
  export default {
    name: 'App',
    data() {
      return {
        cart: []
      }
    },
    components: {
      rad_logo,
      freelancer_navbar, 
      // freelancer_header, 
      freelancer_portfolio
      // freelancer_about, 
      // freelancer_contact,
      // freelancer_footer
      // ,
      // freelancer_copyright
    },
    methods: {
      formatPrice(value) {
        let val = (value/1).toFixed(2).replace('.', ',')
        return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ".")
      },
      updateCart(e) {
            this.cart.push(e);
            // alert(this.cart)
            // this.total = this.shoppingCartTotal;
      },
      upd(e){
        this.cart = e
      },
      sendOrder(cart_){
        var ua = navigator.userAgent.toLowerCase();

        var isMobile = ua.indexOf("mobile") > -1;
        
        if (isMobile) {

            window.location.href = "whatsapp://send?text=Olá gostaria de fazer um pedido:" + JSON.stringify(cart_) + "&phone=5573999539290"

        } else {

            window.open("https://web.whatsapp.com/send?text=Olá gostaria de fazer um pedido:" + JSON.stringify(cart_) + "&phone=5573999539290", "Share with Whatsapp Web", 'width=800,height=600');

        }
        // location.href = "https://api.whatsapp.com/send?phone=73999539290&text=Olá gostaria de fazer um pedido"
      }
    },
    computed: {
        sortedCart() {
            // Return a copy of the sorted array
            // console.log(this.cart)
            return this.cart.filter(function(p){return p.qnt})
        },
        total(){
          var t = 0
          this.cart.forEach(function(a){
            t += parseInt(a.qnt) * parseFloat(a.price)
          })
          console.log(t);
          
          return t
          // return this.cart.filter(function(p){return p.qnt})
        }
    }
  }
</script>
