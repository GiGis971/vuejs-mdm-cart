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
            <MdmCart
              :products="cart.items"
              @addOnItem="incrementQuantityCartItem"
              @removeOneItem="decrementQuantityCartItem"
              class="mb-3"
            />
            <div class="d-flex bg-dark p-2 text-light mb-3">
              <div><strong>Total: </strong></div>
              <div class="ml-auto">
                <strong>{{ parseFloat(totalCart).toFixed(2) }} €</strong>
              </div>
            </div>
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
    },
    totalCart() {
      const total =
        this.cart.items.length > 0
          ? this.cart.items.reduce(
              (total, item) => item.price * item.quantity + total,
              0
            )
          : 0;
      return total;
    }
  },
  mounted() {
    this.products = require("./api/Products");
  },
  methods: {
    addToCart(payload) {
      const cartItem = this.cart.items.find(item => payload.ref === item.ref);
      cartItem
        ? this.incrementQuantityCartItem(cartItem)
        : this.cart.items.push(payload);
    },
    decrementQuantityCartItem(item) {
      item.quantity--;
      if (item.quantity === 0) this.removeCartItem(item);
    },
    incrementQuantityCartItem(item) {
      item.quantity++;
    },
    removeCartItem(item) {
      const index = this.cart.items.findIndex(
        product => product.ref === item.ref
      );
      this.cart.items.splice(index, 1);
    }
  }
};
</script>
