<template>
    <div>
        <header>
            <h1>Nuxt App</h1>
            <nav>
                <ul>
                    <li><nuxt-link to="/">Главная</nuxt-link></li>
                    <li><nuxt-link to="/posts">Все посты</nuxt-link></li>
                    <li><nuxt-link to="/posts/add">Новый пост</nuxt-link></li>
                </ul>
            </nav>
        </header>
        <NuxtPage />
    </div>
</template>

<script setup></script>

<style lang="scss"></style>
