<script>
export default {
  name: "ProductCartItem",
  props: {
    product: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      quantity: 1
    }
  },
  computed: {
    totalSum () {
        return this.quantity * this.product.price
      }
    },
  methods: {
    onDelete(){
      this.$emit('deleteProduct', this.product.id)
    },
    dec() {
      if (this.quantity > 1) {
        this.quantity -= 1
      }
    },
    inc() {
      this.quantity += 1
    }
  },
}
</script>

<template>
  <div class="cart-item">
    <div class="top">
      <div class="image">
        <img :src="product.imgSrc" :alt="product.title"/>
      </div>
      <div class="top-body">
        <div>{{ product.title }}</div>
        <button @click='onDelete'>Видалити</button>
      </div>
    </div>
    <div class="bottom">
      <button class="btn" @click='dec'>-</button>
      {{ quantity }}
      <button class="btn" @click='inc'>+</button>
      <span>{{ totalSum }}</span>
    </div>
  </div>
</template>

<style scoped>
.cart-item {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.btn {
  background-color: green;
  color: white;
  padding: 10px 16px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
}

.top {
  display: flex;
}

.top-body {
  display: flex;
  justify-content: space-between;
  gap: 30px;
}

.top-body button {
  align-self: flex-start;
  background-color: red;
  color: white;
  padding: 10px 16px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
}

.image {
  flex: 0 0 200px;
}

.image img {
  width: 100%;
}

.bottom {
  align-self: flex-end;
  display: flex;
  gap: 10px;
  align-items: center;
}
</style>