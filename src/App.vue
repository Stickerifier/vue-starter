<script setup lang="ts">
import DownloadFile from "./components/DownloadFile.vue";
</script>

<template>
  <div>
    <a href="https://t.me/StickerifyImageBot" target="_blank">
      <img src="/stickerify.svg" class="logo stickerify" alt="Stickerify logo"/>
    </a>
    <a href="https://github.com/Stickerifier/Stickerify" target="_blank">
      <img src="./assets/github.svg" class="logo github" alt="GitHub logo"/>
    </a>
  </div>
  <DownloadFile />
</template>

<style scoped>
.logo {
  height: 6em;
  padding: 1.5em;
  will-change: filter;
  transition: filter 300ms;
}

.logo.stickerify:hover {
  filter: drop-shadow(0 0 2em #48aeceff);
}

.logo.github:hover {
  filter: drop-shadow(0 0 2em #aeb1b1);
}
</style>
