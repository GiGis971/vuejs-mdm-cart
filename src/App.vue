<template>
  <div id="app">
    <MdmNavBar :total-cart-items="totalItem" />
    <section id="mdm-cart" class="my-5">
      <b-container>
        <b-row>
          <b-col>
            <h1 class="display-1 pb-2 border-bottom mb-5">Mon panier</h1>
          </b-col>
        </b-row>
      </b-container>
      <b-container>
        <b-row>
          <b-col cols="8">
            <MdmCart :products="cart.items" class="mb-3" />
            <div class="d-flex">
              <b-button
                variant="outline-warning"
                class="ml-auto mr-3 text-dark"
                @click="cart.items = []"
              >
                Tout supprimer
              </b-button>
              <b-button variant="primary">Valider le panier</b-button>
            </div>
          </b-col>
          <b-col cols="4">
            <MdmProductsRelated :products="products" @selected="addToCart" />
          </b-col>
        </b-row>
      </b-container>
    </section>
  </div>
</template>

<script>
import MdmNavBar from "./components/MdmNavBar.vue";
import MdmProductsRelated from "./components/MdmProductsRelated.vue";
import MdmCart from "./components/MdmCart.vue";

export default {
  name: "app",
  components: {
    MdmNavBar,
    MdmCart,
    MdmProductsRelated
  },
  data() {
    return {
      products: [],
      cart: {
        items: []
      }
    };
  },
  computed: {
    totalItem() {
      return this.cart.items.length;
    }
  },
  mounted() {
    this.products = require("./api/Products");
  },
  methods: {
    addToCart(payload) {
      this.cart.items.push(payload);
    }
  }
};
</script>
