<script setup lang="ts">
import { ref } from 'vue'

const projectId = ref('')
const projectStatus = ref(null)

async function checkProjectStatus() {
  try {
    const response = await fetch(`http://127.0.0.1:8000/project/is-finished?project_id=${projectId.value}`)
    if (response.ok) {
      const data = await response.json()
      projectStatus.value = data.ended
    }
    else {
      console.error('Ошибка при проверке статуса проекта:', response.statusText)
    }
  }
  catch (error) {
    console.error('Ошибка при проверке статуса проекта:', error)
  }
}
</script>

<template>
  <div>
    <h2>Проверка завершения проекта</h2>
    <label for="projectId">ID проекта:</label>
    <input id="projectId" v-model="projectId" type="text" class="styled-input">
    <button class="styled-button" @click="checkProjectStatus">
      Проверить статус проекта
    </button>
    <div v-if="projectStatus !== null">
      <p>Статус проекта: {{ projectStatus ? 'Завершен' : 'Не завершен' }}</p>
    </div>
  </div>
</template>

<style scoped>
.styled-button {
  padding: 10px 20px;
  font-size: 16px;
  text-align: center;
  border: 1px solid #000;
}

.styled-input {
  width: auto;
  padding: 10px;
  margin: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
}
</style>
