<template>
  <div class="py-3 px-2 pb-0 shadow border">
    <div v-if="hasProduct">
      <h2 class="display-5 text-center mt-1">Votre panier est vide</h2>
    </div>
    <div v-else>
      <table class="table thead-dark table-responsive">
        <thead class="thead-dark">
          <tr>
            <th class="w-25 d-none d-md-table-cell">Image</th>
            <th>Produit</th>
            <th>Reference</th>
            <th>Quantités</th>
            <th>Prix</th>
          </tr>
        </thead>
        <tbody v-for="(product, i) in products" :key="i" class="align-middle">
          <tr>
            <td class="w-25 d-none d-md-table-cell">
              <img
                :src="product.image"
                class="w-100"
                :alt="product.title.detail"
              />
            </td>
            <td class="w-50 align-middle">
              {{ product.title.name }} <br />
              <small class="text-secondary">{{ product.title.details }}</small>
            </td>
            <td class="align-middle">
              <small>Ref: {{ product.ref }}</small>
            </td>
            <td class="align-middle text-right">
              <b-button-group>
                <b-button variant="light" @click="removeOneItem(product)">
                  -
                </b-button>
                <b-button variant="disable">
                  {{ product.quantity }}
                </b-button>
                <b-button variant="light" @click="addOnItem(product)">
                  +
                </b-button>
              </b-button-group>
            </td>
            <td class="align-middle">
              {{ parseFloat(product.price).toFixed(2) }}&nbsp;€
            </td>
          </tr>
        </tbody>
      </table>
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
  },
  methods: {
    addOnItem(item) {
      this.$emit("addOnItem", item);
    },
    removeOneItem(item) {
      this.$emit("removeOneItem", item);
    }
  }
};
</script>

<style scoped lang="scss"></style>
