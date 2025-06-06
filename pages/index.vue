<template>
    <div>
        <h1>Главная страница</h1>
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

<style lang="scss"></style>
