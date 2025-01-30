<script>
import {notebooksList} from "@/constants/NotebookList";
import ProductCard
  from "@/components/Products/ProductCard.vue";
import ProductCart
  from "@/components/Products/ProductCart.vue";

export default {
  name: "ProductsCardsList",
  components: {ProductCart, ProductCard},
  data() {
    return {
      purchasersList: []
    }
  },
  computed: {
    productsList() {
      return notebooksList;
    }
  },
  methods: {
    onBuy(productId) {
      const newProduct = this.productsList.find(item => item.id === productId);
      this.purchasersList.push(newProduct);
    },
    onDeleteProduct(productId) {
      this.purchasersList = this.purchasersList.filter(item => item.id !== productId);
    }
  }
}
</script>

<template>
  <div class="container">
    <div class="cards-list">
      <product-card v-for="product in productsList"
                    :key='product.id'
                    :product='product'
                    @buy='onBuy'
      ></product-card>
    </div>
    <div v-if="purchasersList.length > 0" class="cart">
      <product-cart
          :purchasersList='purchasersList'
          @deleteProduct='onDeleteProduct'></product-cart>
    </div>
    <p v-else>Кошик порожній...</p>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  gap: 50px;
}

.cards-list {
  display: flex;
  flex-direction: column;
  gap: 20px;
  max-width: 500px;
}
</style>