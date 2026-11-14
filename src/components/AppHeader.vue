<template>
  <header class="app-header">
    <div class="app-header__content">
      <div class="app-header__brand">
        <h1 class="app-header__title">🛒 Don Pepe</h1>
        <p class="app-header__subtitle">Tu tienda de confianza</p>
      </div>

      <div class="app-header__cart">
        <span>Mi carrito 🛍️</span>
      </div>
    </div>
  </header>
</template>

<style lang="scss" scoped>
@use '../assets/scss/variables' as *;

.app-header {
  background-color: $color-surface;
  border-bottom: 1px solid $color-border;
  padding: 2.5rem 5%;
}

.app-header__content {
  max-width: 1200px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
}

.app-header__brand {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
}

.app-header__title {
  font-size: 3rem;
  color: $color-primary;
}

.app-header__cart {
  background-color: $color-background;
  padding: 1rem 1.5rem;
  border-radius: $radius-medium;
  font-size: 1.5rem;
  font-weight: 600;
  color: $color-text;
}

.app-header__subtitle {
  font-size: 1.3rem;
  color: $color-text-light;
}

@media (min-width: 1024px) {
  .app-header__content {
    flex-direction: row;
    justify-content: space-between;
  }

  .app-header__brand {
    align-items: flex-start;
  }
}


</style>