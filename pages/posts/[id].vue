<template>
    <div>
        <h1>{{ post.title }}</h1>
        <img :src="post.image" alt="Post Image" />
        <p>{{ post.description }}</p>
        <div v-html="post.body"></div>
        <nuxt-link to="/posts">Назад к всем постам</nuxt-link>
        <nuxt-link :to="`/posts/edit/${postId}`">Редактировать пост</nuxt-link>
        <button @click="showModal = true">Удалить пост</button>

        <div v-if="showModal" class="modal">
            <div class="modal-content">
                <h2>Подтверждение удаления</h2>
                <p>Вы уверены, что хотите удалить этот пост?</p>
                <button @click="deletePost">Да, удалить</button>
                <button @click="showModal = false">Отмена</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { useAsyncData } from "nuxt/app";
import { useRoute, useRouter } from "vue-router";
import { ref } from "vue";

const route = useRoute();
const router = useRouter();
const postId = route.params.id;

const { data: post } = await useAsyncData("post", () =>
    $fetch(`http://localhost:3001/posts/${postId}`),
);

const showModal = ref(false);

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
