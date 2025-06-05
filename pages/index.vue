<template>
    <div>
        <h1>Главная страница</h1>
        <PostList
            url="http://localhost:3001/posts?_sort=-id&_order=desc&_limit=3"
        />
    </div>
</template>

<script setup></script>

<style lang="scss"></style>
