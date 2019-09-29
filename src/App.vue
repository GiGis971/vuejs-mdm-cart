<template>
  <div id="app">
    <MdmNavBar />
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
            <MdmCart :products="cart.items" />
          </b-col>
          <b-col cols="4">
            <MdmProductsRelated :products="products" />
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
  mounted() {
    this.products = require("./api/Products");
  }
};
</script>
