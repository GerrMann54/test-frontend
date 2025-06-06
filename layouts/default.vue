<template>
    <div class="app-container">
        <header class="app-header">
            <h1 class="app-title">Nuxt App</h1>
            <nav class="app-nav">
                <ul class="nav-list">
                    <li class="nav-item">
                        <nuxt-link to="/">Главная</nuxt-link>
                    </li>
                    <li class="nav-item">
                        <nuxt-link to="/posts">Все посты</nuxt-link>
                    </li>
                    <li class="nav-item">
                        <nuxt-link to="/posts/add">Новый пост</nuxt-link>
                    </li>
                </ul>
            </nav>
        </header>
        <NuxtPage />
    </div>
</template>

<script setup>
import { useHead } from "nuxt/app";
import { ref, provide } from "vue";

const metaTitle = ref("Nuxt App");
const metaDesc = ref("Meta Desc");
provide("metaTitle", metaTitle);
provide("metaDesc", metaDesc);

useHead({
    title: metaTitle,
    meta: [
        { charset: "utf-8" },
        { name: "viewport", content: "width=device-width, initial-scale=1.0" },
        {
            name: "description",
            content: metaDesc,
        },
    ],
});
</script>

<style lang="scss">
$app-bg-color: #121212; // Темный фон
$app-text-color: #e0e0e0; // Светлый текст
$app-accent-color: #a8e600; // Ярко-лаймовый акцент

.app-container {
    background-color: $app-bg-color;
    color: $app-text-color;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    font-family: sans-serif;
}

.app-header {
    background-color: darken($app-bg-color, 5%);
    padding: 20px;
    display: flex;
    justify-content: space-between;
    align-items: center;
}

.app-title {
    font-size: 2rem;
    margin: 0;
}

.app-nav {
    .nav-list {
        list-style: none;
        padding: 0;
        display: flex;
        gap: 20px;
    }

    .nav-item {
        a {
            color: $app-accent-color;
            text-decoration: none;
            transition: color 0.3s;

            &:hover {
                color: lighten($app-accent-color, 10%);
            }
        }
    }
}

NuxtPage {
    flex: 1;
    padding: 20px;
}
</style>
