<template>
    <div>
        <div v-for="post in posts" :key="post.id">
            <h2>{{ post.title }}</h2>
            <p>{{ post.description }}</p>
            <nuxt-link :to="`/posts/${post.id}`">Читать далее</nuxt-link>
        </div>
    </div>
</template>

<script setup>
defineProps(["posts"]);
</script>

<style scoped></style>
