<template>
  <div class="detalle-producto">
    <button class="btn-volver" @click="$emit('volver')">← Volver al catálogo</button>
    
    <div class="detalle-contenedor">
      <div class="detalle-imagen">
        <img :src="producto.imagen" :alt="producto.nombre">
        
        <!-- CONTROL PARA SUBIR TU PROPIA IMAGEN -->
        <div class="subir-foto-box">
          <label :for="'upload-' + producto.id" class="btn-subir-foto">
            📷 Cambiar Foto de la Zapatilla
          </label>
          <input 
            type="file" 
            :id="'upload-' + producto.id" 
            accept="image/*" 
            @change="cambiarImagenLocal" 
            style="display: none;"
          />
        </div>
      </div>
      
      <div class="detalle-info">
        <span v-if="producto.nuevo" class="badge nuevo">Nuevo Ingreso</span>
        <span v-if="producto.oferta" class="badge oferta">¡Precio Especial!</span>
        
        <h2>{{ producto.nombre }}</h2>
        <p class="categoria">Calzado de Performance / Básquet</p>
        <p class="descripcion">{{ producto.descripcion }}</p>
        
        <div class="precio-seccion">
          <p v-if="producto.oferta" class="precio-anterior">Antes: ${{ producto.precioOriginal }}</p>
          <p class="precio-actual">${{ producto.precio }}</p>
        </div>

        <!-- Al hacer clic emite el producto para guardarlo en el carrito global -->
        <button class="btn-comprar" @click="$emit('agregar-al-carrito', producto)">
          Añadir al carrito
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['producto'],
  methods: {
    cambiarImagenLocal(event) {
      const archivo = event.target.files[0];
      if (archivo) {
        // Convierte el archivo seleccionado de tu pc en una URL temporal legible por el navegador
        const urlNuevaImagen = URL.createObjectURL(archivo);
        
        // Le enviamos la nueva URL al componente App.vue para que actualice la zapatilla
        this.$emit('actualizar-imagen-producto', {
          id: this.producto.id,
          nuevaImagen: urlNuevaImagen
        });
      }
    }
  }
}
</script>

<style scoped>
/* Tus estilos anteriores se mantienen */
.btn-volver {
  background-color: #333;
  color: white;
  border: none;
  padding: 10px 15px;
  cursor: pointer;
  border-radius: 4px;
  margin-bottom: 20px;
}
.detalle-contenedor {
  display: flex;
  gap: 40px;
  background-color: #262626;
  padding: 30px;
  border-radius: 12px;
  flex-wrap: wrap;
}
.detalle-imagen {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 15px;
}
.detalle-imagen img {
  max-width: 350px;
  width: 100%;
  border-radius: 8px;
  height: auto;
  object-fit: cover;
}
/* Estilo del botón subir foto */
.subir-foto-box {
  width: 100%;
}
.btn-subir-foto {
  display: block;
  text-align: center;
  background-color: #444;
  color: #fff;
  padding: 8px 12px;
  border-radius: 6px;
  cursor: pointer;
  font-size: 13px;
  transition: background-color 0.2s;
}
.btn-subir-foto:hover {
  background-color: #555;
}
.detalle-info {
  flex: 1;
  min-width: 280px;
}
.badge {
  padding: 4px 10px;
  font-size: 12px;
  font-weight: bold;
  border-radius: 20px;
}
.badge.nuevo { background-color: #ff4500; color: white; }
.badge.oferta { background-color: #e6c300; color: black; }
.categoria { color: #888; font-style: italic; }
.precio-actual { font-size: 26px; color: #ff4500; font-weight: bold; }
.btn-comprar {
  background-color: #ff4500;
  color: white;
  border: none;
  padding: 15px 25px;
  font-size: 16px;
  font-weight: bold;
  cursor: pointer;
  border-radius: 6px;
}
</style>