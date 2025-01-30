<script>
import ProductCartItem
  from "@/components/Products/ProductCartItem.vue";

export default {
  name: "ProductCart",
  components: {ProductCartItem},
  props: {
    purchasersList: {
      type: Array,
      required: true
    }
  },
}
</script>

<template>
  <h2>Кошик</h2>
  <div class="cart">
    <product-cart-item v-for="product in purchasersList"
                       :key="product.id"
                       :product='product'
                       @totalSum='onTotalSum'
                       @deleteProduct="$emit('deleteProduct', $event)"
    ></product-cart-item>
  </div>
</template>

<style scoped>
.cart {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>