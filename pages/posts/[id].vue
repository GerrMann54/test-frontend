<template>
    <div>
        <h1>{{ post.title }}</h1>
        <img :src="post.image" alt="Post Image" />
        <p>{{ post.description }}</p>
        <div v-html="post.body"></div>
        <nuxt-link to="/posts">Назад к всем постам</nuxt-link>
    </div>
</template>

<script setup>
import { useAsyncData } from "nuxt/app";
import { useRoute } from "vue-router";

const route = useRoute();
const postId = route.params.id;
const { data: post } = await useAsyncData("post", () =>
    $fetch(`http://localhost:3001/posts/${postId}`),
);
</script>

<style lang="scss"></style>
