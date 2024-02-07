<template>
  <div class="app-container">
    <!-- Contenido de tu aplicación aquí -->  
    <div class="container">
    <h1>Producción de Video Profesional</h1>

    <div class="select-container">
      <label for="service-select">Selecciona un Servicio:</label>
      <select v-model="selectedOption" id="service-select" class="select">
        <option value="fifteen">Producción de Video para Fiestas de 15</option>
        <option value="wedding">Producción de Video para Bodas</option>
        <option value="prom">Producción de Video para Egresados</option>
      </select>
    </div>

    <div class="form-container">
      <component :is="selectedOption === 'fifteen' ? FifteenBudgetDetail : 
                   selectedOption === 'wedding' ? WeddingBudgetDetail : 
                   selectedOption === 'prom' ? PromBudgetDetail : null" />
    </div>
  </div>
  </div>
</template>

<script lang="ts" setup>

import { ref } from 'vue';
import FifteenBudgetDetail from './components/FifteenBudgetDetail.vue';
import WeddingBudgetDetail from './components/WeddingBudgetDetail.vue';
import PromBudgetDetail from './components/PromBudgetDetail.vue';

const selectedOption = ref('fifteen'); // Opción seleccionada por defecto

</script>


<style>
.container {
  max-width: 800px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Arial', sans-serif;
}

h1 {
  text-align: center;
  color: #333;
}

.select-container {
  margin-bottom: 20px;
}

.select-container label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

.select {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 2px solid #333;
  border-radius: 5px;
  background-color: #fff;
  color: #333;
  cursor: pointer;
}

.select option {
  background-color: #fff;
  color: #333;
}

.form-container {
  margin-top: 20px;
}

/* Estilos responsivos */
@media screen and (max-width: 600px) {
  .container {
    padding: 10px;
  }
}

.app-container {
  /* Establecer la imagen de fondo */
  background-image: url('https://scontent.fcor3-1.fna.fbcdn.net/v/t1.6435-9/70396637_10216853300858820_7895593591764942848_n.jpg?_nc_cat=104&ccb=1-7&_nc_sid=2be8e3&_nc_eui2=AeEKokZV9TQVAxc0oo5nYFM6-BCT7CxfWav4EJPsLF9Zq5NMV6nD4Dd_LJlizC6ATgQ&_nc_ohc=mv3jN7EFaIsAX9dDpQB&_nc_ht=scontent.fcor3-1.fna&oh=00_AfD1Ftnnsy_P_iDQpokEi8lOAEesfj9Px7eEYoI7T6_p6w&oe=65EA588A');
  /* Establecer el tamaño y posición de la imagen de fondo */
  background-size: cover;
  background-position: center;
  /* Establecer la opacidad */
  opacity: 0.7; /* Ajusta el valor de 0 a 1 según la opacidad deseada */
}
</style>
