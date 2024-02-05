<template>
    <h1>Ejemplo de v-if</h1>
    <h1 v-if="age<18">Eres menor de edad</h1>
    <h1 v-else>Eres mayor de edad</h1>
</template>

<script lang="ts" setup>
let age = 32

    
</script>

<style scoped>
</style>