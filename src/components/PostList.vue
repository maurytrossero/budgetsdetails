<template>
    <div class="container">
        <PostDetail v-for="elem in info" :key="elem.title"/>
    </div>
  
</template>

<script lang="ts" setup>
import PostDetail from './PostDetail.vue';
interface Post{
    title: string,
    content: string
}

let info:Array<Post> = [{
        title: "Este es el post 1",
        content: "Texto de ejemplo 1"
        },
        {
            title: "Este es el post 2",
            content: "Texto de ejemplo 2"
        },
        {
            title: "Este es el post 3",
            content: "Texto de ejemplo 3"
        },
        {
            title: "Este es el post 4",
            content: "Texto de ejemplo 4"
        },
        {
            title: "Este es el post 4",
            content: "Texto de ejemplo 5"
        }
    ]


</script>

<style scoped>
.container{
    display: flex;
    flex-wrap: wrap;
    flex-direction: row;
    justify-content: space-around;
}
</style>
  