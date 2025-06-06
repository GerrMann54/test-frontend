<template>
    <div>
        <div v-for="post in posts" :key="post.id">
            <h2>{{ post.title }}</h2>
            <img :src="post.image" alt="Post Image" />
            <p>{{ post.description }}</p>
            <nuxt-link :to="`/posts/${post.id}`">Читать далее</nuxt-link>
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

<style lang="scss"></style>
