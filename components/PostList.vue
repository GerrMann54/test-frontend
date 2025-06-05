<template>
    <div>
        <div v-for="post in posts" :key="post.id">
            <h2>{{ post.title }}</h2>
            <img :src="post.image" alt="Post Image" />
            <p>{{ post.description }}</p>
            <nuxt-link :to="`/posts/${post.id}`">Читать далее</nuxt-link>
        </div>
    </div>
</template>

<script setup>
import { useAsyncData } from "nuxt/app";

const props = defineProps({
    url: {
        type: String,
        required: true,
    },
});

const { data: posts } = await useAsyncData("posts", () => $fetch(props.url));
</script>

<style lang="scss"></style>
