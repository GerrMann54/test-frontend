<template>
    <div>
        <h1>Редактировать пост</h1>
        <form @submit.prevent="updatePost">
            <div>
                <label for="title">Заголовок:</label>
                <input type="text" v-model="post.title" required />
            </div>
            <div>
                <label for="image">Ссылка на изображение:</label>
                <input type="text" v-model="post.image" required />
            </div>
            <div>
                <label for="description">Описание:</label>
                <textarea v-model="post.description" required></textarea>
            </div>
            <div>
                <label for="body">Содержимое:</label>
                <textarea v-model="post.body" required></textarea>
            </div>
            <button type="submit">Сохранить изменения</button>
        </form>
        <nuxt-link to="/posts">Назад к всем постам</nuxt-link>
    </div>
</template>

<script setup>
import { useRoute, useRouter } from "vue-router";
import { useAsyncData } from "nuxt/app";

const route = useRoute();
const router = useRouter();
const postId = route.params.id;

const { data: post } = await useAsyncData("post", () =>
    $fetch(`http://localhost:3001/posts/${postId}`),
);

const title = inject("metaTitle");
const desc = inject("metaDesc");
title.value = post.value.title;
desc.value = post.value.description;
console.log(post);

const updatePost = async () => {
    try {
        await $fetch(`http://localhost:3001/posts/${postId}`, {
            method: "PUT",
            body: post.value,
        });
        router.push(`/posts/${postId}`);
    } catch (error) {
        console.error("Ошибка при обновлении поста:", error);
    }
};
</script>

<style lang="scss"></style>
