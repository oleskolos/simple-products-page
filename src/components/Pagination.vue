<template>
  <div class="pagination">
    <button :disabled="currentPage === 1" @click="$emit('change-page', currentPage - 1)">
      &lt;
    </button>
    <button
      v-for="n in totalPages"
      :key="n"
      :class="{ active: n === currentPage }"
      @click="$emit('change-page', n)"
    >
      {{ n }}
    </button>
    <button :disabled="currentPage === totalPages" @click="$emit('change-page', currentPage + 1)">
      &gt;
    </button>
  </div>
</template>

<script setup>
defineProps(['currentPage', 'totalPages'])
</script>

<style scoped>
.pagination {
  display: flex;
  gap: 0.5rem;
  justify-content: center;
  margin-top: 1rem;
}
button {
  padding: 0.5rem 1rem;
  border: 1px solid #ccc;
}
button.active {
  background-color: #333;
  color: white;
}
</style>
