<script setup lang="ts">
import {ref} from 'vue';

const fileId = ref('');

const handleSubmit = () => {
  const botToken = import.meta.env.VITE_STICKERIFY_TOKEN;
  const fileInfoApi = `https://api.telegram.org/bot${botToken}/getFile?file_id=${fileId.value}`;

  fetch(fileInfoApi)
    .then(response => response.json())
    .then(data => {
      const filePath = data.result.file_path;
      const fileName = filePath.split('/')[1];
      const downloadFileApi = `https://api.telegram.org/file/bot${botToken}/${filePath}`;

      fetch(downloadFileApi)
        .then(response => response.blob())
        .then(blob => {
          const url = URL.createObjectURL(blob);
          const element = document.createElement('a');
          element.href = url;
          element.download = fileName;
          document.body.appendChild(element);
          element.click();
          URL.revokeObjectURL(url);
          document.body.removeChild(element);
        })
        .catch(error => {
          console.error('An error occurred downloading the file %s:', fileName, error);
        });
    })
    .catch(error => {
      console.error('Unexpected failure:', error);
    });
};
</script>

<template>
  <h1>Stickerify Triager</h1>

  <form @submit.prevent="handleSubmit">
    <div>
      <label for="fileId">Enter the fileId: </label>
      <input type="text" id="fileId" v-model="fileId" required>
    </div>
    <button type="submit">Download file</button>
  </form>
</template>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  gap: 2em;
}

button {
  align-self: auto;
}
</style>
