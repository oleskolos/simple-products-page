<template>
  <div class="container">
    <CategoryFilter :categories="['All', ...categories]" v-model="selectedCategory" />
    <div class="grid">
      <ProductCard
        v-for="product in paginatedProducts"
        :key="product.id"
        :product="product"
      />
    </div>
    <Pagination
      :current-page="currentPage"
      :total-pages="totalPages"
      @change-page="currentPage = $event"
    />
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import ProductCard from '../components/ProductCard.vue'
import CategoryFilter from '../components/CategoryFilter.vue'
import Pagination from '../components/Pagination.vue'

const products = ref([])
const categories = ref([])
const selectedCategory = ref('All')
const currentPage = ref(1)
const productsPerPage = 10

const fetchProducts = async () => {
  const res = await fetch('https://fakestoreapi.com/products')
  products.value = await res.json()
}

const fetchCategories = async () => {
  const res = await fetch('https://fakestoreapi.com/products/categories')
  categories.value = await res.json()
}

onMounted(() => {
  fetchProducts()
  fetchCategories()
})

const filteredProducts = computed(() =>
  selectedCategory.value === 'All'
    ? products.value
    : products.value.filter(p => p.category === selectedCategory.value)
)

const totalPages = computed(() =>
  Math.ceil(filteredProducts.value.length / productsPerPage)
)

const paginatedProducts = computed(() => {
  const start = (currentPage.value - 1) * productsPerPage
  return filteredProducts.value.slice(start, start + productsPerPage)
})
</script>

<style scoped>
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 1rem;
}
.grid {
  display: grid;
  grid-gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}
</style>
