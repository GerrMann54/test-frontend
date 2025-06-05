<template>
    <div>
        <header>
            <h1>Nuxt App</h1>
            <nav>
                <nuxt-link to="/">Главная</nuxt-link>
                <nuxt-link to="/posts">Все посты</nuxt-link>
                <nuxt-link to="/posts/add">Новый пост</nuxt-link>
            </nav>
        </header>
        <NuxtPage />
    </div>
</template>

<script setup></script>

<style lang="scss"></style>
