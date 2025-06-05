<template>
    <div>
        <h1>{{ post.title }}</h1>
        <img :src="post.image" alt="Post Image" />
        <p>{{ post.description }}</p>
        <div v-html="post.body"></div>
        <nuxt-link to="/posts">Назад к всем постам</nuxt-link>
        <button @click="deletePost">Удалить пост</button>
    </div>
</template>

<script setup>
import { useAsyncData } from "nuxt/app";
import { useRoute, useRouter } from "vue-router";

const route = useRoute();
const router = useRouter();
const postId = route.params.id;

const { data: post } = await useAsyncData("post", () =>
    $fetch(`http://localhost:3001/posts/${postId}`),
);

const deletePost = async () => {
    try {
        await $fetch(`http://localhost:3001/posts/${postId}`, {
            method: "DELETE",
        });
        router.push("/posts");
    } catch (error) {
        console.error("Ошибка при удалении поста:", error);
    }
};
</script>

<style lang="scss"></style>
