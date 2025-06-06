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

<style lang="scss"></style>
