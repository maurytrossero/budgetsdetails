<template>
    <form>
        <input type="text" v-model="inputText"/>
        <input type="checkbox" v-model="agree"/> Acepto los terminos y condiciones
        <select v-model="country">
            <option value="Argentina">Argentina</option>
            <option value="Brasil">Brasil</option>
            <option value="Uruguay">Uruguay</option>
        </select>
    </form>
</template>

<script lang="ts" setup>
import { Ref, ref } from 'vue'
let inputText:Ref<string> = ref('')
let agree: Ref<boolean> = ref(true)
let country: Ref<string> = ref('Argentina')
</script>

<style scoped>
.danger{
    color: red;
}
</style>