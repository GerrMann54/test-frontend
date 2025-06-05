<template>
    <div>
        <h1>Создать новый пост</h1>
        <form @submit.prevent="createPost">
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
            <button type="submit">Создать пост</button>
        </form>
        <nuxt-link to="/posts">Назад к всем постам</nuxt-link>
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

<style lang="scss"></style>
