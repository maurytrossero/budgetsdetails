<template>
    <h3> {{ counter }}</h3>
    <button @click="addCounter" class="btn-counter">Incrementar</button>
    <button @click="quitCounter" class="btn-counter">Decrementar</button>
</template>

<script lang="ts" setup>
import { Ref, ref } from 'vue';
let counter:Ref = ref(0)
const addCounter = ():void => {
    counter.value++
}
const quitCounter = ():void => {
    counter.value--
 }

</script>

<style scoped>
    /* Agregamos los estilos del botón */
    .btn-counter {
        display: inline-block;
        padding: 10px 20px;
        font-size: 16px;
        font-weight: bold;
        text-align: center;
        text-decoration: none;
        cursor: pointer;
        border-radius: 5px;
        background-color: #3498db;
        color: #fff;
        border: 2px solid #2980b9;
        transition: background-color 0.3s, color 0.3s, border-color 0.3s;
        margin-right: 10px; /* Añadido para separar los botones */
    }

    /* Estilos cuando se pasa el ratón sobre el botón */
    .btn-counter:hover {
        background-color: #2980b9;
        border-color: #3498db;
        color: #fff;
    }
</style>