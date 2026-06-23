<template>
  <div class="inicio">
    <div class="hero-banner">
      <h1>BIENVENIDO A KICKSZONE</h1>
      <p>Las mejores zapatillas de básquet del mercado para romper las redes.</p>
    </div>

    <h2>🔥 Nuevos Ingresos</h2>
    <div class="grid-productos">
      <div 
        v-for="p in productos" 
        :key="p.id" 
        class="tarjeta-producto" 
        @click="$emit('seleccionar-producto', p)"
      >
        <img :src="p.imagen" :alt="p.nombre">
        <h3>{{ p.nombre }}</h3>
        <p class="precio">${{ p.precio }}</p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['productos']
}
</script>

<style scoped>
.hero-banner {
  background: linear-gradient(135deg, #ff4500, #b22222);
  padding: 40px;
  border-radius: 12px;
  text-align: center;
  margin-bottom: 40px;
}

.hero-banner h1 {
  margin: 0 0 10px 0;
  font-size: 32px;
  letter-spacing: 2px;
}

.grid-productos {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(220px, 1fr));
  gap: 20px;
}

.tarjeta-producto {
  background-color: #262626;
  border-radius: 8px;
  padding: 15px;
  text-align: center;
  cursor: pointer;
  transition: transform 0.2s, box-shadow 0.2s;
}

.tarjeta-producto:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(255, 69, 0, 0.3);
}

.tarjeta-producto img {
  max-width: 100%;
  border-radius: 4px;
}

.precio {
  font-size: 18px;
  color: #ff4500;
  font-weight: bold;
  margin: 10px 0 0 0;
}
</style>