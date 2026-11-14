<script setup>
defineProps({
  product: {
    type: Object,
    required: true,
  },
});
</script>

<template>
  <article
    class="product-card"
    :class="{ 'product-card--out-of-stock': product.stock === 0 }"
  >
    <div class="product-card__emoji">
      {{ product.emoji }}
    </div>

    <h3>{{ product.nombre }}</h3>

    <p>Precio: ${{ product.precio.toLocaleString("es-CO") }}</p>

    <p>Stock disponible: {{ product.stock }}</p>

    <span v-if="product.stock === 0"> Agotado </span>
  </article>
</template>

<style lang="scss" scoped>
@use "../assets/scss/variables" as *;

.product-card {
  background-color: $color-surface;
  border: 1px solid $color-border;
  border-radius: $radius-large;
  padding: 2rem;
  box-shadow: $shadow-card;
  transition: transform 0.2s ease;

  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.product-card:hover {
  transform: translateY(-4px);
}

.product-card__emoji {
  font-size: 4rem;
  text-align: center;
}

.product-card h3 {
  font-size: 1.8rem;
  color: $color-text;
}

.product-card p {
  font-size: 1.4rem;
  color: $color-text-light;
}

.product-card span {
  color: $color-danger;
  font-size: 1.4rem;
  font-weight: 700;
}

.product-card--out-of-stock {
  background-color: #ECEFEC;
  opacity: 0.75;
}

.product-card--out-of-stock:hover {
  transform: none;
}
</style>
