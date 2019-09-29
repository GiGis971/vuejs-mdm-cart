<template>
  <div class="py-3 px-2 pb-0 shadow border">
    <div v-if="hasProduct">
      <h2>Votre panier est vide</h2>
    </div>
    <div v-else>
      {{ products }}
    </div>
  </div>
</template>

<script>
export default {
  name: "MdmCart",
  props: {
    products: {
      type: Array,
      required: false,
      default() {
        return [];
      }
    }
  },
  computed: {
    hasProduct() {
      return this.products.length <= 0;
    }
  }
};
</script>

<style scoped lang="scss"></style>
