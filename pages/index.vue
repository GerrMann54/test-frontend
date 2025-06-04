<template>
    <div>
        <h1>Главная страница</h1>
        <PostList :posts="posts" />
    </div>
</template>

<script setup>
import { useAsyncData } from "nuxt/app";

const { data: posts } = await useAsyncData("posts", () =>
    $fetch("http://localhost:3001/posts?_sort=-id&_order=desc&_limit=3"),
);
</script>

<style lang="scss"></style>
