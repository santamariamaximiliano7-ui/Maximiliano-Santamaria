<template>
  <div class="app-container">
    <Navbar 
      :vista="vistaActual" 
      :cantidadCarrito="carrito.length" 
      @cambiar-vista="irAVista" 
    />

    <main class="contenido">
      <Inicio 
        v-if="vistaActual === 'inicio'" 
        :productos="nuevosIngresos" 
        @seleccionar-producto="verDetalle" 
      />

      <Productos 
        v-if="vistaActual === 'productos'" 
        :productos="listaProductos" 
        @seleccionar-producto="verDetalle" 
      />

      <Ofertas 
        v-if="vistaActual === 'ofertas'" 
        :productos="productosEnOferta" 
        @seleccionar-producto="verDetalle" 
      />

      <Contactos v-if="vistaActual === 'contactos'" />

      <CarritoView 
        v-if="vistaActual === 'carrito'" 
        :items="carrito" 
        @eliminar-del-carrito="quitarDelCarrito" 
      />

      <DetalleProducto 
        v-if="vistaActual === 'detalle'" 
        :producto="productoSeleccionado" 
        @volver="vistaActual = vistaPrevia" 
        @agregar-al-carrito="añadirAlCarrito"
      />
    </main>
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue'
import Inicio from './components/Inicio.vue'
import Productos from './components/Productos.vue'
import Ofertas from './components/Ofertas.vue'
import DetalleProducto from './components/DetalleProducto.vue'
import Contactos from './components/Contactos.vue'
import CarritoView from './components/CarritoView.vue'

export default {
  components: {
    Navbar,
    Inicio,
    Productos,
    Ofertas,
    DetalleProducto,
    Contactos,
    CarritoView
  },
  data() {
    return {
      vistaActual: 'inicio',
      vistaPrevia: 'productos',
      productoSeleccionado: null,
      carrito: [], // Almacena los productos agregados
      
      // BASE DE DATOS DE PRODUCTOS CON LINKS DE INTERNET ESTABLES Y CORREGIDOS
      listaProductos: [
        { 
          id: 1, 
          nombre: 'Air Jordan 4 Retro', 
          precio: 210, 
          imagen: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTh3-GEPHZXRw9rJiazxMzpS8k3JfOhZ5qPMHDs-hD-CATYINKtwYCqhZ32&s=10', 
          descripcion: 'Un clásico indiscutible tanto en el asfalto como en el parqué. Amortiguación Air-Sole premium de máxima respuesta.', 
          nuevo: true, 
          oferta: false 
        },
        { 
          id: 2, 
          nombre: 'LeBron XXI "Akoya"', 
          precio: 200, 
          imagen: 'https://i.shgcdn.com/3f221fd3-1feb-49e9-8e4a-3612e7d4c578/-/format/auto/-/preview/3000x3000/-/quality/lighter/', 
          descripcion: 'Diseñadas para soportar la intensidad del juego de impacto. Máxima estabilidad con cables zonales.', 
          nuevo: true, 
          oferta: false 
        },
        { 
          id: 3, 
          nombre: 'KD 16 "Aura"', 
          precio: 130, 
          precioOriginal: 160, 
          imagen: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSg6vaKEZaIrfWA_RWUYHVQcojjI-cL5foalHUM02gOAg-9dqSoC2mtGs2-&s=10', 
          descripcion: 'Unidad Nike Air superior combinada con amortiguación elástica ideal para tiradores letales.', 
          nuevo: false, 
          oferta: true 
        },
        { 
          id: 4, 
          nombre: 'Curry Flow 11 "Future"', 
          precio: 140, 
          precioOriginal: 175, 
          imagen: 'https://www.dexter.com.ar/on/demandware.static/-/Sites-365-dabra-catalog/default/dw4b58d959/products/UA3026617-300/UA3026617-300-6.JPG', 
          descripcion: 'Tracción sin goma totalmente revolucionaria. Sentí el control total en cada cambio de ritmo.', 
          nuevo: false, 
          oferta: true 
        },
        { 
          id: 5, 
          nombre: 'Nike Freak 5 "Giannis"', 
          precio: 150, 
          imagen: 'https://www.dexter.com.ar/on/demandware.static/-/Sites-365-dabra-catalog/default/dwb11882ad/products/NIDX4985-600/NIDX4985-600-6.JPG', 
          descripcion: 'Velocidad impresionante para primeros pasos explosivos. El diseño te mantiene pegado al parqué.', 
          nuevo: true, 
          oferta: false 
        },
        { 
          id: 6, 
          nombre: 'Jordan Tatum 2 "Vortex"', 
          precio: 125, 
          precioOriginal: 150, 
          imagen: 'https://images.stockx.com/360/Air-Jordan-2-Tatum-Vortex-GS/Images/Air-Jordan-2-Tatum-Vortex-GS/Lv2/img01.jpg?w=480&q=60&dpr=1&updated_at=1757402239&h=320', 
          descripcion: 'Estructura ultraliviana para reducir el desgaste en la cancha con soportes laterales de espuma.', 
          nuevo: false, 
          oferta: true 
        },
        { 
          id: 7, 
          nombre: 'Luka 2 "Nebula"', 
          precio: 140, 
          imagen: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcScDXASBUvUjv-Dr7OrA4qt7DwupxfaRD01DwCf7srdC_T6CQE1ifkrBNE&s=10', 
          descripcion: 'Diseñadas para el juego de control, frenos bruscos y step-backs mortales. Soporte firme de 360 grados.', 
          nuevo: true, 
          oferta: false 
        },
        { 
          id: 8, 
          nombre: 'Kyrie Infinity', 
          precio: 110, 
          precioOriginal: 140, 
          imagen: 'https://www.dexter.com.ar/on/demandware.static/-/Sites-365-dabra-catalog/default/dw4744f42c/products/NI_DH5385-900/NI_DH5385-900-6.JPG', 
          descripcion: 'Ajuste personalizado y tracción científica en los bordes para los cambios de dirección más extremos.', 
          nuevo: false, 
          oferta: true 
        }
      ]
    }
  },
  computed: {
    nuevosIngresos() {
      return this.listaProductos.filter(p => p.nuevo);
    },
    productosEnOferta() {
      return this.listaProductos.filter(p => p.oferta);
    }
  },
  methods: {
    irAVista(nombreVista) {
      this.vistaActual = nombreVista;
    },
    verDetalle(producto) {
      this.vistaPrevia = this.vistaActual;
      this.productoSeleccionado = producto;
      this.vistaActual = 'detalle';
    },
    añadirAlCarrito(producto) {
      this.carrito.push(producto);
      alert(`¡${producto.nombre} agregado al carrito!`);
    },
    quitarDelCarrito(index) {
      this.carrito.splice(index, 1);
    }
  }
}
</script>

<style>
body {
  margin: 0;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  background-color: #1a1a1a;
  color: #ffffff;
}

.contenido {
  padding: 30px 20px;
  max-width: 1200px;
  margin: 0 auto;
}
</style>