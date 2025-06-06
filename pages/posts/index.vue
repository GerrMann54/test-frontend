<template>
    <div>
        <h1>Все посты</h1>
        <PostList url="http://localhost:3001/posts" />
    </div>
</template>

<script setup>
import { inject } from "vue";
const title = inject("metaTitle");
const desc = inject("metaDesc");
title.value = "Все посты";
desc.value = "Описание";
</script>

<style lang="scss"></style>
