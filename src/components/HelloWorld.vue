<script setup lang="ts">
defineProps<{ msg: string }>();
</script>

<template>
  <!-- <div class="read-the-docs"> -->
<div class="defaultTemp">
  <h1>{{ msg }}</h1>

<p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank">create-vue</a>, the official Vue + Vite starter
</p>
<p>
    Install
    <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
    in your IDE for a better DX
</p>
<p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</div>

</template>

<style scoped>
.read-the-docs {
    color: #888;
}
</style>
