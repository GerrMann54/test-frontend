<template>
    <div class="create-post-page">
        <h1 class="page-title">Редактировать пост</h1>
        <form @submit.prevent="updatePost" class="post-form">
            <div class="form-group">
                <label for="title" class="form-label">Заголовок:</label>
                <input
                    type="text"
                    v-model="post.title"
                    required
                    class="form-input"
                />
            </div>
            <div class="form-group">
                <label for="image" class="form-label"
                    >Ссылка на изображение:</label
                >
                <input
                    type="text"
                    v-model="post.image"
                    required
                    class="form-input"
                />
            </div>
            <div class="form-group">
                <label for="description" class="form-label">Описание:</label>
                <textarea
                    v-model="post.description"
                    required
                    class="form-textarea"
                ></textarea>
            </div>
            <div class="form-group">
                <label for="body" class="form-label">Содержимое:</label>
                <textarea
                    v-model="post.body"
                    required
                    class="form-textarea"
                ></textarea>
            </div>
            <button type="submit" class="submit-button">Сохранить</button>
        </form>
        <nuxt-link to="/posts" class="back-link">Назад к всем постам</nuxt-link>
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
