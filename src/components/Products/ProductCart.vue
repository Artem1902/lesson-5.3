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
  computed: {
    orderSum (){
      return this.purchasersList.reduce((acc, cur) => acc + (cur.price * cur.quantity), 0);
    }
  },
  methods: {
    onSubmit(){
      alert ('Успіх!')
    }
  }
}
</script>

<template>
  <h2>Кошик</h2>
  <div class="cart">
    <product-cart-item v-for="product in purchasersList"
                       :key="product.id"
                       :product='product'
                       @deleteProduct="$emit('deleteProduct', $event)"
                       @quantity = "$emit('quantity', $event)"
    ></product-cart-item>
    <div class="sum">
      Загальна сума покупки: {{orderSum}}$
    </div>
    <button @click = 'onSubmit' class="btn">Оформити замовлення</button>
  </div>
</template>

<style scoped>
.cart {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
.btn {
  background-color: green;
  color: white;
  padding: 10px 16px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
}
</style>