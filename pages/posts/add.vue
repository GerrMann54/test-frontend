<template>
    <div class="create-post-page">
        <h1 class="page-title">Создать новый пост</h1>
        <form @submit.prevent="createPost" class="post-form">
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
            <button type="submit" class="submit-button">Создать пост</button>
        </form>
        <nuxt-link to="/posts" class="back-link">Назад к всем постам</nuxt-link>
    </div>
</template>

<script setup>
import { ref } from "vue";
import { useRouter } from "vue-router";

const post = ref({
    title: "",
    image: "",
    description: "",
    body: "",
});

import { inject } from "vue";
const title = inject("metaTitle");
const desc = inject("metaDesc");
title.value = "Новый пост";
desc.value = "Описание страницы";

const router = useRouter();

const createPost = async () => {
    try {
        await $fetch("http://localhost:3001/posts", {
            method: "POST",
            body: post.value,
        });
        router.push("/posts");
    } catch (error) {
        console.error("Ошибка при создании поста:", error);
    }
};
</script>

<style lang="scss">
$page-bg-color: #121212;
$page-text-color: #e0e0e0;
$page-accent-color: #a8e600;

.create-post-page {
    background-color: $page-bg-color;
    color: $page-text-color;
    padding: 20px;
    border-radius: 5px;
}

.page-title {
    font-size: 2rem;
    margin-bottom: 20px;
}

.post-form {
    background-color: $page-bg-color;
    padding: 20px;
    border-radius: 5px;
    max-width: 600px;
}

.form-group {
    margin-bottom: 15px;
}

.form-label {
    display: block;
    margin-bottom: 5px;
}

.form-input,
.form-textarea {
    width: 100%;
    padding: 10px;
    border: 1px solid $page-accent-color;
    border-radius: 4px;
    background-color: #1e1e1e;
    color: $page-text-color;

    &:focus {
        border-color: lighten($page-accent-color, 10%);
        outline: none;
    }
}

.form-textarea {
    height: 100px;
}

.submit-button {
    background-color: $page-accent-color;
    color: white;
    border: none;
    padding: 10px 15px;
    cursor: pointer;
    transition: background-color 0.3s;
}

.back-link {
    display: inline-block;
    margin-top: 20px;
    color: $page-accent-color;
    text-decoration: none;
}
</style>
