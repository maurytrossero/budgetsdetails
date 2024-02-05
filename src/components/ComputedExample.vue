<template>
    <div class="container">
      <form @submit.prevent="submitForm" class="vat-form">
        <label for="subtotal">Subtotal:</label>
        <input type="number" v-model="subtotal" id="subtotal" class="subtotal-input">
        <button type="submit" class="calculate-button">Calcular Impuestos</button>
      </form>
      <div class="result-box">
        <h3>Total de impuestos a pagar:</h3>
        <p class="result-text">{{ totalVat.toFixed(2) }} {{ vat }}%</p>
      </div>
    </div>
  </template>
  
  <script lang="ts" setup>
  import { Ref, ref, computed } from 'vue';
  
  const vat = 21;
  let subtotal: Ref<number> = ref(0);
  const totalVat = computed(() => (vat * subtotal.value) / 100);
  
  const submitForm = () => {
    // Puedes realizar acciones adicionales al enviar el formulario si lo necesitas
  };
  </script>
  
  <style scoped>
  .container {
    max-width: 400px;
    margin: 0 auto;
    text-align: center;
  }
  
  .vat-form {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 20px;
  }
  
  .subtotal-input {
    padding: 8px;
    font-size: 16px;
    margin-top: 8px;
  }
  
  .calculate-button {
    margin-top: 16px;
    padding: 10px;
    background-color: #4CAF50; /* Color verde */
    color: #fff;
    border: none;
    cursor: pointer;
    transition: background-color 0.3s ease;
  }
  
  .calculate-button:hover {
    background-color: #45a049; /* Cambio de color al pasar el ratón */
  }
  
  .result-box {
    background-color: #f9f9f9;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  }
  
  .result-text {
    margin-top: 10px;
    font-size: 18px;
    color: #333;
    font-weight: bold;
  }
  </style>
  