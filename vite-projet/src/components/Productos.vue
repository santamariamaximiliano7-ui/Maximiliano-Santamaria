<template>
  <div class="productos">
    <h2>👟 Catálogo de Zapatillas</h2>
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
  transition: transform 0.2s;
}

.tarjeta-producto:hover {
  transform: translateY(-5px);
}

.tarjeta-producto img {
  max-width: 100%;
  border-radius: 4px;
}

.precio {
  font-size: 18px;
  color: #ff4500;
  font-weight: bold;
}
</style>