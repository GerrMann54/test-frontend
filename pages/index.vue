<template>
    <div class="main-container">
        <h1 class="main-title">Главная страница</h1>
        <PostList
            url="http://localhost:3001/posts?_sort=-id&_order=desc&_limit=3"
        />
    </div>
</template>

<script setup>
import { inject } from "vue";
const title = inject("metaTitle");
const desc = inject("metaDesc");
title.value = "Главная страница";
desc.value = "Описание страницы";
</script>

<style lang="scss">
.main-container {
    padding: 20px;
    background-color: #121212;
    color: #e0e0e0;
}

.main-title {
    font-size: 2rem;
    margin-bottom: 20px;
    color: #a8e600;
}
</style>
