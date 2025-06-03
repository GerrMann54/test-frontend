<template>
    <div>
        <h1>Все посты</h1>
        <div v-for="post in posts" :key="post.id">
            <h2>{{ post.title }}</h2>
            <p>{{ post.description }}</p>
            <nuxt-link :to="`/posts/${post.id}`">Читать далее</nuxt-link>
        </div>
        <nuxt-link to="/">На главную</nuxt-link>
    </div>
</template>

<script setup>
import { useAsyncData } from "nuxt/app";

const { data: posts } = await useAsyncData("posts", () =>
    $fetch("http://localhost:3001/posts"),
);
</script>

<style lang="scss">
/* Здесь можно добавить стили для страницы всех постов */
</style>
