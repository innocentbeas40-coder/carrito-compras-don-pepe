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