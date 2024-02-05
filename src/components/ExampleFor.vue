<template>
    <h1>Ejemplo de v-for</h1>
    <ul>
        <li v-for="country in countries" :key="country.codigo"> {{ country.nombre }}</li>
    </ul>

</template>

<script lang="ts" setup>
import { Ref, ref} from 'vue';
let countries:Ref<Array<{codigo: string; nombre: string}>> = ref([
    { codigo: 'AR', nombre: 'Argentina' },
    { codigo: 'BR', nombre: 'Brasil' },
    { codigo: 'CA', nombre: 'Canadá' },
    { codigo: 'CL', nombre: 'Chile' },
    { codigo: 'CO', nombre: 'Colombia' },
    { codigo: 'CR', nombre: 'Costa Rica' },
    { codigo: 'CU', nombre: 'Cuba' },
    { codigo: 'DO', nombre: 'República Dominicana' },
    { codigo: 'EC', nombre: 'Ecuador' },
    { codigo: 'GT', nombre: 'Guatemala' },
    { codigo: 'HN', nombre: 'Honduras' },
    { codigo: 'MX', nombre: 'México' },
    { codigo: 'NI', nombre: 'Nicaragua' },
    { codigo: 'PA', nombre: 'Panamá' },
    { codigo: 'PE', nombre: 'Perú' },
    { codigo: 'PY', nombre: 'Paraguay' },
    { codigo: 'US', nombre: 'Estados Unidos' },
    { codigo: 'UY', nombre: 'Uruguay' },
    { codigo: 'VE', nombre: 'Venezuela' },
    { codigo: 'BO', nombre: 'Bolivia' }
])
</script>

<style scoped>

</style>