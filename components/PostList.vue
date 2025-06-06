<template>
    <div class="post-list">
        <div v-for="post in posts" :key="post.id" class="post-card">
            <img :src="post.image" alt="Post Image" class="post-image" />
            <div class="post-content">
                <h2 class="post-title">{{ post.title }}</h2>
                <p class="post-description">{{ post.description }}</p>
                <nuxt-link :to="`/posts/${post.id}`" class="read-more"
                    >Читать далее</nuxt-link
                >
            </div>
        </div>
    </div>
</template>

<script setup>
import { useAsyncData } from "nuxt/app";
import { ref } from "vue";

const props = defineProps({
    url: {
        type: String,
        required: true,
    },
});

const url = ref(props.url);

const { data: posts } = await useAsyncData(
    `posts-${url.value}`,
    () => $fetch(url.value),
    {
        watch: [url],
    },
);
</script>

<style lang="scss">
$post-bg-color: #1e1e1e; // Цвет фона карточки
$post-title-color: #a8e600; // Ярко-лаймовый цвет заголовка
$post-text-color: #e0e0e0; // Цвет текста

.post-list {
    display: grid;
    grid-template-columns: repeat(
        auto-fill,
        minmax(300px, 1fr)
    ); // Адаптивная сетка
    gap: 20px; // Отступы между карточками
}

.post-card {
    background-color: $post-bg-color;
    border-radius: 8px;
    overflow: hidden; // Скрыть переполнение
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.3);
    transition: transform 0.3s;

    &:hover {
        transform: translateY(-5px); // Эффект при наведении
    }
}

.post-image {
    width: 100%;
    height: auto;
}

.post-content {
    padding: 15px;
}

.post-title {
    font-size: 1.5rem;
    color: $post-title-color;
    margin: 0 0 10px 0;
}

.post-description {
    color: $post-text-color;
    margin: 10px 0;
}

.read-more {
    color: $post-title-color;
    text-decoration: none;
    font-weight: bold;
    transition: color 0.3s;

    &:hover {
        color: lighten($post-title-color, 10%);
    }
}
</style>
