<template>
    <div class="post-card">
        <h3>Titulo</h3>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Eos illum ex illo, cumque sequi repudiandae beatae quam debitis rerum quis minus alias, fuga at obcaecati 
            nam in? Aut, fugiat libero. Lorem ipsum dolor sit amet consectetur adipisicing elit. Eos illum ex illo, cumque sequi repudiandae beatae quam debitis rerum quis minus alias, fuga at obcaecati 
            nam in? Aut, fugiat libero</p>
        <PostBtn/>
    </div>
</template>

<script lang="ts" setup>
    import PostBtn from './PostBtn.vue';
</script>

<style scoped>

.post-card{
    border-radius: 15px;
    padding: 10px;
    margin: 5px;
    border: 1px solid #ccc;
}
</style>