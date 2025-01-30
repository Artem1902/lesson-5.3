<script>
export default {
  name: "ProductCard",
  props: {
    product: {
      type: Object,
      required: true
    }
  },
  methods: {
    onBuy(){
      this.$emit('buy', this.product.id);
    }
  }
}
</script>

<template>
  <div class="card">
    <div class="image">
      <a :href="product.link">
        <img :src="product.imgSrc" :alt="product.title">
      </a>
    </div>
    <div class="content">
      <a :href="product.link">
        <h2>{{ product.title }}</h2>
      </a>
      <div class="body">
        <div class="price">
          <p>Ваша економія:
            <span class="discount">
            {{ product.discount }}$
            </span>
          </p>
          <p class="oldPrice">{{ product.oldPrice }}$</p>
          <p class="newPrice">{{ product.price }}$</p>
        </div>
        <div class="btn">
          <button @click='onBuy'>Купити</button>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
.card {
  display: flex;
  gap: 20px
}

.image {
  flex: 0 0 200px;
}

.image img {
  width: 100%;
}

.content {
  flex: 1 1 auto;
}

.body {
  display: flex;
  justify-content: space-between;
}

.btn {
  align-self: flex-end;
}

.btn button {
  background-color: green;
  color: white;
  padding: 10px 16px;
  border: none;
  border-radius: 10px;
  cursor: pointer;
}

.discount {
  color: red
}

.newPrice {
  font-size: 28px;
  color: red
}

.oldPrice {
  text-decoration: line-through;
  opacity: 0.5;
}
</style>