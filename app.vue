<template>
  <ul>
    <li><nuxt-link to="/">Index</nuxt-link></li>
    <li><nuxt-link to="/about">About</nuxt-link></li>
    <li><nuxt-link to="/about2">Invalid path 1</nuxt-link></li>
    <li><nuxt-link :to="'/about2'">Invalid path 2</nuxt-link></li>
    <li><nuxt-link :to="{name: 'about2'}">Invalid path 3</nuxt-link></li>
  </ul>
  <hello-world></hello-world>
  <nuxt-page></nuxt-page>
</template>

<script setup lang="ts">
// Uncomment this and `nuxt-typed-router` errors will disappear:
// import {HelloWorld} from '#components';
// You don't event have to import anything:
// import {} from '#components';
</script>
