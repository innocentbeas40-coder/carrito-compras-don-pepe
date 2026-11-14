
<script setup>
defineProps({
  carrito: {
    type: Array,
    required: true
  },
  subtotal: {
    type: Number,
    required: true
  },
  descuento: {
    type: Number,
    required: true
  },
  total: {
    type: Number,
    required: true
  }
})

const emit = defineEmits(['eliminar'])
</script>

<template>
  <section class="shopping-cart">
    <h2>Mi carrito 🛒</h2>

    <p v-if="carrito.length === 0" class="cart-empty">
      Tu carrito está vacío.
    </p>

    <div v-else class="cart-products">
      <div
        v-for="producto in carrito"
        :key="producto.id"
        class="cart-product"
      >
        <span class="cart-product__emoji">
          {{ producto.emoji }}
        </span>

        <span class="cart-product__name">
          {{ producto.nombre }}
        </span>

        <span class="cart-product__quantity">
          Cantidad: {{ producto.cantidad }}
        </span>

        <span class="cart-product__subtotal">
          ${{ (producto.precio * producto.cantidad).toLocaleString('es-CO') }}
        </span>

        <button
          class="cart-product__remove"
          @click="emit('eliminar', producto)"
        >
          ✕
        </button>
      </div>
    </div>

    <div class="cart-summary">
      <div class="cart-total">
        <h3>Subtotal:</h3>
        <p>${{ subtotal.toLocaleString('es-CO') }}</p>
      </div>

      <div class="cart-total">
        <h3>Descuento (10%):</h3>
        <p>${{ descuento.toLocaleString('es-CO') }}</p>
      </div>

      <div class="cart-total cart-total--final">
        <h3>Total a pagar:</h3>
        <p>${{ total.toLocaleString('es-CO') }}</p>
      </div>

      <p v-if="subtotal < 50000 && subtotal > 0" class="cart-message">
        ¡Agrega más productos para obtener un 10% de descuento desde $50.000!
      </p>
    </div>
  </section>
</template>

<style lang="scss" scoped>
@use '../assets/scss/variables' as *;

.shopping-cart {
  max-width: 1200px;
  margin: 3rem auto;
  padding: 2.5rem;
  background-color: $color-surface;
  border: 1px solid $color-border;
  border-radius: $radius-large;
  box-shadow: $shadow-card;
}

.shopping-cart h2 {
  font-size: 2.2rem;
  color: $color-primary;
  margin-bottom: 2rem;
}

.cart-empty {
  font-size: 1.5rem;
  color: $color-text-light;
  text-align: center;
  padding: 2rem 0;
}

.cart-products {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
}

.cart-product {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 1rem;
  padding: 1.5rem 0;
  border-bottom: 1px solid $color-border;
}

.cart-product__emoji {
  font-size: 2.5rem;
}

.cart-product__name {
  font-size: 1.5rem;
  font-weight: 600;
  color: $color-text;
}

.cart-product__quantity {
  font-size: 1.4rem;
  color: $color-text-light;
}

.cart-product__subtotal {
  font-size: 1.5rem;
  font-weight: 700;
  color: $color-primary;
}

.cart-product__remove {
  background-color: $color-danger;
  color: white;
  border: none;
  border-radius: $radius-small;
  padding: 0.8rem 1.2rem;
  font-size: 1.5rem;
  cursor: pointer;
}

.cart-summary {
  margin-top: 2rem;
  border-top: 1px solid $color-border;
  padding-top: 1rem;
}

.cart-total {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 1rem;
  padding: 1rem 0;
}

.cart-total h3 {
  font-size: 1.6rem;
  color: $color-text;
}

.cart-total p {
  font-size: 1.6rem;
  font-weight: 600;
  color: $color-primary;
}

.cart-total--final {
  border-top: 1px solid $color-border;
  margin-top: 1rem;
  padding-top: 2rem;
}

.cart-total--final h3,
.cart-total--final p {
  font-size: 2rem;
  font-weight: 700;
}

.cart-message {
  font-size: 1.3rem;
  color: $color-text-light;
  text-align: center;
  margin-top: 1rem;
}
</style>
