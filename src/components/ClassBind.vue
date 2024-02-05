<template>
    <p :class="{ 'danger' : hasError}">El mensaje se ha enviado correctamente</p>
    <button @click=handleClick()>Cambiar Color</button>

    <p :style="{ backgroundColor: '#ccc', color:c }">Ha ocurrido un error</p>

</template>

<script lang="ts" setup>
import {ref} from 'vue'
    let hasError = true;
    let c = ref('#fff'); 
    const handleClick = ()=> {c.value = '#ff0000'}

</script>

<style scoped>
.danger{
    color: red;
}
</style>