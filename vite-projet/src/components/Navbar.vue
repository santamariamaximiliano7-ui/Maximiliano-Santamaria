<template>
  <header class="navbar">
    <div class="logo">🏀 KicksZone</div>
    <nav>
      <button :class="{ activo: vista === 'inicio' }" @click="cambiarVista('inicio')">Inicio</button>
      <button :class="{ activo: vista === 'productos' }" @click="cambiarVista('productos')">Productos</button>
      <button :class="{ activo: vista === 'ofertas' }" @click="cambiarVista('ofertas')">Ofertas</button>
      <button :class="{ activo: vista === 'contactos' }" @click="cambiarVista('contactos')">Contactos</button>
      <!-- Botón del Carrito con Contador -->
      <button :class="{ activo: vista === 'carrito', 'btn-carrito': true }" @click="cambiarVista('carrito')">
        🛒 Carrito <span v-if="cantidadCarrito > 0" class="contador">{{ cantidadCarrito }}</span>
      </button>
    </nav>
  </header>
</template>

<script>
export default {
  props: ['vista', 'cantidadCarrito'],
  methods: {
    cambiarVista(nuevaVista) {
      this.$emit('cambiar-vista', nuevaVista);
    }
  }
}
</script>

<style scoped>
.navbar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background-color: #111;
  border-bottom: 2px solid #ff4500;
}

.logo {
  font-size: 24px;
  font-weight: bold;
  color: #ff4500;
}

nav {
  display: flex;
  align-items: center;
}

nav button {
  background: none;
  border: none;
  color: #ccc;
  margin-left: 15px;
  font-size: 16px;
  cursor: pointer;
  transition: color 0.3s;
  padding: 5px 10px;
  position: relative;
}

nav button:hover, nav button.activo {
  color: #ff4500;
  font-weight: bold;
}

.btn-carrito {
  background-color: #222;
  border-radius: 20px;
  padding: 6px 14px;
  border: 1px solid #333;
}

.contador {
  background-color: #ff4500;
  color: white;
  font-size: 12px;
  font-weight: bold;
  border-radius: 50%;
  padding: 2px 7px;
  margin-left: 5px;
}
</style>