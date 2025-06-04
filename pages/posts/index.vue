<template>
    <div>
        <h1>Все посты</h1>
        <PostList :posts="posts" />
    </div>
</template>

<script setup>
import { useAsyncData } from "nuxt/app";

const { data: posts } = await useAsyncData("posts", () =>
    $fetch("http://localhost:3001/posts"),
);
</script>

<style lang="scss"></style>
