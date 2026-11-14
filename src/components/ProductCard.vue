<script setup>
defineProps({
  product: {
    type: Object,
    required: true
  }
})
</script>

<template>
  <article class="product-card">
    <div class="product-card__emoji">
      {{ product.emoji }}
    </div>

    <h3>{{ product.nombre }}</h3>

    <p>Precio: ${{ product.precio.toLocaleString('es-CO') }}</p>

    <p>Stock disponible: {{ product.stock }}</p>

    <span v-if="product.stock === 0">
      Agotado
    </span>
  </article>
</template>