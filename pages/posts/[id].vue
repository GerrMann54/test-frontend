<template>
    <div class="post-page">
        <h1 class="post-title">{{ post.title }}</h1>
        <img :src="post.image" alt="Post Image" class="post-image" />
        <div v-html="post.body" class="post-body"></div>
        <ul class="post-actions">
            <li>
                <nuxt-link to="/posts" class="action-link">Назад</nuxt-link>
            </li>
            <li>
                <nuxt-link :to="`/posts/edit/${postId}`" class="action-link"
                    >Редактировать</nuxt-link
                >
            </li>
            <li>
                <a @click="showModal = true" class="action-link">Удалить</a>
            </li>
        </ul>

        <div v-if="showModal" class="modal">
            <div class="modal-content">
                <h2>Удалить пост?</h2>
                <p>Вы уверены?</p>
                <button @click="deletePost" class="confirm-button">Да</button>
                <button @click="showModal = false" class="cancel-button">
                    Нет
                </button>
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

<style lang="scss">
$post-bg-color: #121212;
$post-text-color: #e0e0e0;
$post-accent-color: #a8e600;

.post-page {
    background-color: $post-bg-color;
    color: $post-text-color;
    padding: 20px;
    max-width: 800px;
    margin: 0 auto;
}

.post-title {
    font-size: 2.5rem;
    margin-bottom: 20px;
}

.post-image {
    max-width: 100%;
    height: auto;
    margin-bottom: 20px;
}

.post-body {
    margin-bottom: 20px;
}

.post-actions {
    list-style: none;
    padding: 0;
    display: flex;
    gap: 15px;

    .action-link {
        color: $post-accent-color;
        text-decoration: none;
        transition: color 0.3s;
        cursor: pointer;

        &:hover {
            color: lighten($post-accent-color, 10%);
        }
    }
}

.modal {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;

    .modal-content {
        background-color: $post-bg-color;
        padding: 20px;
        border-radius: 5px;
        text-align: center;

        h2 {
            margin: 0 0 10px;
        }

        .confirm-button,
        .cancel-button {
            margin: 5px;
            padding: 10px 15px;
            border: none;
            cursor: pointer;
        }

        .confirm-button {
            background-color: $post-accent-color;
            color: white;
        }

        .cancel-button {
            background-color: darken($post-accent-color, 10%);
            color: white;
        }
    }
}
</style>
