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
      let isAlreadyAdded = this.purchasersList.some(item => item.id === productId);
      if (!isAlreadyAdded) {
        let newProduct = this.productsList.find(item => item.id === productId);
        newProduct = {...newProduct, quantity: 1};
        this.purchasersList.push(newProduct);
      } else {
        let findInPurchase = this.purchasersList.find(item => item.id === productId);
        findInPurchase.quantity += 1;
      }

    },
    onDeleteProduct(productId) {
      this.purchasersList = this.purchasersList.filter(item => item.id !== productId);
    },
    changeQuantity({prodId, quantity}) {
      let product = this.purchasersList.find(item => item.id === prodId);
      product.quantity = product.quantity + quantity;
      console.log(this.purchasersList)
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
          @deleteProduct='onDeleteProduct'
          @quantity='changeQuantity'
      ></product-cart>
    </div>
    <p v-else>Кошик порожній...</p>
  </div>
</template>

<style scoped>
.container {
  display: flex;
  gap: 50px;
  max-width: 1020px;
}

.cards-list {
  display: flex;
  flex-direction: column;
  gap: 20px;
  max-width: 500px;
}
</style>