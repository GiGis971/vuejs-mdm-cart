<template>
  <div>
    <h2 class="h6">Produits en relation :</h2>
    <div>
      <b-container fluid>
        <b-row v-for="(product, i) in products" :key="i" class="mb-5">
          <b-col>
            <img
              :src="product.image"
              class="w-100"
              :alt="product.title.details"
            />
          </b-col>
          <b-col>
            <strong>
              {{ product.title.name }} - {{ product.title.details }}
            </strong>
            <div class="text-secondary font-weight-bold mb-2">
              {{ product.price }} €
            </div>
            <b-button @click="addToCart(products)">
              <small>Ajouter au panier</small>
            </b-button>
          </b-col>
        </b-row>
      </b-container>
    </div>
  </div>
</template>

<script>
export default {
  name: "MdmProductsRelated",
  props: {
    products: {
      required: true,
      type: Array
    }
  },
  methods: {
    addToCart(payload) {
      this.$emit("selected", { ...payload });
    }
  }
};
</script>

<style scoped lang="scss"></style>
