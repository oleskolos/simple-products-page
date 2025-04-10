<template>
  <div class="card">
    <img :src="product.image" :alt="product.title" />
    <h3>{{ product.category }}</h3>
    <p>{{ product.title }}</p>
    <p>⭐ {{ product.rating.rate }} ({{ product.rating.count }})</p>
    <p><strong>€{{ product.price }}</strong></p>
    <div class="actions">
      <input type="number" min="1" v-model="quantity" />
      <button>Add to Cart</button>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
defineProps(['product'])
const quantity = ref(1)
</script>

<style scoped>
.card {
  border: 1px solid #ddd;
  padding: 1rem;
  border-radius: 8px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
img {
  max-height: 150px;
  object-fit: contain;
  margin-bottom: 1rem;
}
.actions {
  display: flex;
  gap: 0.5rem;
  align-items: center;
}
input {
  width: 50px;
}
</style>
