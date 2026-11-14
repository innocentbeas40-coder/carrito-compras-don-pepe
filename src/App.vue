<script setup>
import { ref, computed } from "vue";
import { products } from "./data/products";
import ProductCard from "./components/ProductCard.vue";
import AppHeader from "./components/AppHeader.vue";
import ShoppingCart from "./components/ShoppingCart.vue";

const productos = ref(products);
const carrito = ref([]);

// Calcular la cantidad total de artículos
const cantidadArticulos = computed(() => {
  return carrito.value.reduce((total, producto) => {
    return total + producto.cantidad;
  }, 0);
});

// Calcular el subtotal de la compra
const subtotal = computed(() => {
  return carrito.value.reduce((total, producto) => {
    return total + producto.precio * producto.cantidad;
  }, 0);
});

// Aplicar descuento del 10% desde $50.000
const descuento = computed(() => {
  return subtotal.value >= 50000 ? subtotal.value * 0.1 : 0;
});

// Calcular el total a pagar
const total = computed(() => {
  return subtotal.value - descuento.value;
});

// Agregar productos al carrito
function agregarAlCarrito(producto) {
  if (producto.stock <= 0) return;

  const productoEnCarrito = carrito.value.find(
    (item) => item.id === producto.id,
  );

  if (productoEnCarrito) {
    productoEnCarrito.cantidad++;
  } else {
    carrito.value.push({
      ...producto,
      cantidad: 1,
    });
  }

  producto.stock--;
}

// Eliminar productos y devolver unidades al inventario
function eliminarDelCarrito(producto) {
  const productoOriginal = productos.value.find(
    (item) => item.id === producto.id,
  );

  if (productoOriginal) {
    productoOriginal.stock += producto.cantidad;
  }

  carrito.value = carrito.value.filter((item) => item.id !== producto.id);
}
</script>

<template>
  <main class="app">
    <AppHeader :cantidad="cantidadArticulos" />

    <section class="products">
      <ProductCard
        v-for="p in productos"
        :key="p.id"
        :product="p"
        @agregar="agregarAlCarrito"
      />
    </section>

    <ShoppingCart
      :carrito="carrito"
      :subtotal="subtotal"
      :descuento="descuento"
      :total="total"
      @eliminar="eliminarDelCarrito"
    />
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
