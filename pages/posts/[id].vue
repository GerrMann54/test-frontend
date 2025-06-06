<template>
    <div>
        <h1>{{ post.title }}</h1>
        <img :src="post.image" alt="Post Image" />
        <!-- <p>{{ post.description }}</p> -->
        <!-- Удалено, описание переехало в meta desc -->
        <div v-html="post.body"></div>
        <ul>
            <li><nuxt-link to="/posts">Назад к всем постам</nuxt-link></li>
            <li>
                <nuxt-link :to="`/posts/edit/${postId}`"
                    >Редактировать пост</nuxt-link
                >
            </li>
            <li><button @click="showModal = true">Удалить пост</button></li>
        </ul>

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
import { inject } from "vue";

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
