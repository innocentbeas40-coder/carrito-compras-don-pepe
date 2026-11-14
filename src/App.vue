<script setup>
import { ref } from 'vue'
import { products } from './data/products'
import ProductCard from './components/ProductCard.vue'
import AppHeader from './components/AppHeader.vue'
import ShoppingCart from './components/ShoppingCart.vue'

const productos = ref(products)
</script>

<template>
  <main class="app">
    <AppHeader />

    <section class="products">
      <ProductCard
        v-for="p in productos"
        :key="p.id"
        :product="p"
      />
    </section>

    <ShoppingCart />
  </main>
</template>

<style lang="scss" scoped>

.products {
  max-width: 1200px;
  margin: 0 auto;
  padding: 3rem 2rem;
  text-align: center;

  display: grid;
  grid-template-columns: 1fr;
  gap: 2rem;
}

@media (min-width: 1024px) {
  .products {
    grid-template-columns: repeat(3, 1fr);
  }
}
</style>