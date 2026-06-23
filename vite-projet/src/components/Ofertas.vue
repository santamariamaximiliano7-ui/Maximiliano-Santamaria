<template>
  <div class="ofertas">
    <h2>⚡ Ofertas Imperdibles</h2>
    <div class="grid-productos">
      <div 
        v-for="p in productos" 
        :key="p.id" 
        class="tarjeta-producto" 
        @click="$emit('seleccionar-producto', p)"
      >
        <span class="etiqueta-oferta">OFERTA</span>
        <img :src="p.imagen" :alt="p.nombre">
        <h3>{{ p.nombre }}</h3>
        <div class="precios-box">
          <p class="precio-viejo">${{ p.precioOriginal }}</p>
          <p class="precio">${{ p.precio }}</p>
        </div>
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
  position: relative;
  transition: transform 0.2s;
}

.tarjeta-producto:hover {
  transform: translateY(-5px);
}

.tarjeta-producto img {
  max-width: 100%;
  border-radius: 4px;
}

.etiqueta-oferta {
  position: absolute;
  top: 10px;
  left: 10px;
  background-color: #e6c300;
  color: black;
  font-weight: bold;
  padding: 3px 8px;
  font-size: 11px;
  border-radius: 4px;
}

.precios-box {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
}

.precio-viejo {
  text-decoration: line-through;
  color: #888;
  margin: 0;
}

.precio {
  font-size: 18px;
  color: #2ecc71;
  font-weight: bold;
  margin: 0;
}
</style>