<template>
  <div class="carrito-vista">
    <h2>🛒 Tu Carrito de Compras</h2>
    
    <div v-if="items.length === 0" class="carrito-vacio">
      <p>Tu carrito está vacío. ¡Anda a la sección de productos a buscar tus zapas!</p>
    </div>

    <div v-else class="carrito-contenido">
      <div class="lista-items">
        <div v-for="(item, index) in items" :key="index" class="item-carrito">
          <img :src="item.imagen" :alt="item.nombre" class="img-mini">
          <div class="item-info">
            <h4>{{ item.nombre }}</h4>
            <p class="precio">${{ item.precio }}</p>
          </div>
          <button class="btn-eliminar" @click="$emit('eliminar-del-carrito', index)">❌</button>
        </div>
      </div>

      <div class="resumen-compra">
        <h3>Resumen</h3>
        <hr>
        <div class="fila-resumen">
          <span>Productos ({{ items.length }}):</span>
          <span>${{ totalPagar }}</span>
        </div>
        <div class="fila-resumen total">
          <span>Total:</span>
          <span>${{ totalPagar }}</span>
        </div>
        <button class="btn-finalizar" @click="finalizarCompra">Finalizar Compra</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['items'],
  computed: {
    totalPagar() {
      return this.items.reduce((acc, item) => acc + item.precio, 0);
    }
  },
  methods: {
    finalizarCompra() {
      alert("🏀 ¡Pedido recibido! Preparando tus zapatillas para la cancha.");
    }
  }
}
</script>

<style scoped>
.carrito-vacio {
  text-align: center;
  padding: 40px;
  background-color: #262626;
  border-radius: 8px;
  color: #aaa;
}

.carrito-contenido {
  display: flex;
  gap: 30px;
  flex-wrap: wrap;
}

.lista-items {
  flex: 2;
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.item-carrito {
  display: flex;
  align-items: center;
  background-color: #262626;
  padding: 15px;
  border-radius: 8px;
  gap: 20px;
}

.img-mini {
  width: 70px;
  height: 70px;
  object-fit: cover;
  border-radius: 6px;
}

.item-info {
  flex-grow: 1;
}

.item-info h4 {
  margin: 0 0 5px 0;
  font-size: 18px;
}

.item-info .precio {
  color: #ff4500;
  font-weight: bold;
  margin: 0;
}

.btn-eliminar {
  background: none;
  border: none;
  cursor: pointer;
  font-size: 16px;
}

.resumen-compra {
  flex: 1;
  background-color: #111;
  padding: 20px;
  border-radius: 8px;
  border: 1px solid #333;
  height: max-content;
  min-width: 250px;
}

.resumen-compra h3 {
  margin-top: 0;
}

hr {
  border: 0;
  border-top: 1px solid #333;
  margin: 15px 0;
}

.fila-resumen {
  display: flex;
  justify-content: space-between;
  margin-bottom: 10px;
  color: #ddd;
}

.total {
  font-size: 20px;
  font-weight: bold;
  color: #fff;
  margin-top: 15px;
}

.btn-finalizar {
  width: 100%;
  background-color: #2ecc71;
  color: white;
  border: none;
  padding: 12px;
  font-size: 16px;
  font-weight: bold;
  border-radius: 6px;
  cursor: pointer;
  margin-top: 15px;
  transition: background-color 0.2s;
}

.btn-finalizar:hover {
  background-color: #27ae60;
}
</style>