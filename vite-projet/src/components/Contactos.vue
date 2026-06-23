<template>
  <div class="contactos">
    <h2>📩 Contactate con KicksZone</h2>
    <div class="contacto-contenedor">
      <div class="info-tarjeta">
        <h3>📍 Ubicación y Canchas</h3>
        <p>Encontranos en nuestro Showroom o mandanos un mensaje para coordinar la entrega.</p>
        <p><strong>Email:</strong> info@kickszone.com</p>
        <p><strong>WhatsApp:</strong> +54 9 11 1234-5678</p>
        <p><strong>Instagram:</strong> @KicksZone_básquet</p>
      </div>
      
      <div class="info-tarjeta">
        <h3>⏰ Horarios de Atención</h3>
        <p>Lunes a Viernes: 09:00 a 20:00 hs</p>
        <p>Sábados: 10:00 a 14:00 hs</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.contacto-contenedor {
  display: flex;
  gap: 20px;
  margin-top: 20px;
  flex-wrap: wrap;
}
.info-tarjeta {
  background-color: #262626;
  padding: 25px;
  border-radius: 8px;
  flex: 1;
  min-width: 280px;
  border-left: 4px solid #ff4500;
}
h2 {
  color: #fff;
}
h3 {
  color: #ff4500;
  margin-top: 0;
}
p {
  color: #ddd;
  line-height: 1.6;
}
</style>