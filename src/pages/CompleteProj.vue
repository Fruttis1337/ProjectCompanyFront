<script setup>
import { ref } from 'vue'
import axios from 'axios'

const projectId = ref(null)
const endDate = ref(null)
const completionStatus = ref(null)

async function completeProject() {
  try {
    const response = await axios.patch(`http://127.0.0.1:8000/complete-project/${projectId.value}/`, {
      end_date: endDate.value,
    })
    if (response.data === true)
      completionStatus.value = 'Проект успешно завершен.'
    else
      completionStatus.value = 'Проект не найден.'
  }
  catch (error) {
    console.error('Ошибка при завершении проекта', error)
  }
}
</script>

<template>
  <div>
    <h2>Завершить проект</h2>
    <form @submit.prevent="completeProject">
      <label for="projectId">ID проекта:</label>
      <input id="projectId" v-model="projectId" type="number" required>

      <label for="endDate">Дата завершения проекта:</label>
      <input id="endDate" v-model="endDate" type="date" required>

      <button type="submit">
        Завершить проект
      </button>
    </form>
    <div v-if="completionStatus" class="completion-status">
      <h3>Статус завершения проекта:</h3>
      <p>{{ completionStatus }}</p>
    </div>
  </div>
</template>

<style scoped>
h2 {
  font-size: 1.5rem;
  margin-bottom: 1rem;
}

form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

label {
  font-weight: bold;
  margin-top: 0.5rem;
}

input {
  width: auto;
  margin-bottom: 1rem;
  padding: 0.5rem;
  font-size: 1rem;
  border: 1px solid #ccc;
}

button {
  width: auto;
  padding: 0.5rem 1rem;
  font-size: 1rem;
  border: 1px solid #000;
  background-color: #007BFF;
  color: #fff;
  cursor: pointer;
}

button:hover {
  background-color: #0056b3;
}

.completion-status {
  font-size: 1rem;
  margin-top: 1rem;
}
</style>
