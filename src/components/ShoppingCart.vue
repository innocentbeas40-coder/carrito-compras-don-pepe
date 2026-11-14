<template>
  <section class="shopping-cart">
    <h2>Mi carrito 🛒</h2>

    <p v-if="true">
      Tu carrito está vacío.
    </p>
  </section>
</template>

<style lang="scss" scoped>
@use '../assets/scss/variables' as *;

.shopping-cart {
  background-color: $color-surface;
  border: 1px solid $color-border;
  border-radius: $radius-large;
  padding: 2.5rem;
  box-shadow: $shadow-card;
  margin-top: 3rem;
}

.shopping-cart h2 {
  font-size: 2.2rem;
  color: $color-primary;
  margin-bottom: 2rem;
}

.shopping-cart p {
  font-size: 1.5rem;
  color: $color-text-light;
  text-align: center;
  padding: 2rem 0;
}
</style>