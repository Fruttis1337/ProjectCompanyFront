<script setup>
import { ref } from 'vue'
import axios from 'axios'

const project_id = ref('')
const start_date = ref('')
const end_date = ref('')

function addProjectExecution() {
  // Здесь мы создаем объект, аналогичный вашему схеме ProjectExecutionCreate
  const requestData = {
    project_id: project_id.value,
    start_date: start_date.value,
    end_date: end_date.value, // Это поле будет отправлено, если оно заполнено, или останется undefined
  }

  axios
    .post('/project-execution/', requestData)
    .then((response) => {
      // eslint-disable-next-line no-console
      console.log('Исполнение проекта успешно добавлено', response.data)
    })
    .catch((error) => {
      // Обработка ошибки
      console.error('Произошла ошибка при добавлении исполнения проекта', error)
    })
}
</script>

<template>
  <div class="styled-input-container">
    <label class="styled-label">Добавить исполнение проекта</label>
    <input v-model="project_id" class="styled-input" placeholder="ID проекта">
    <input v-model="start_date" class="styled-input" type="date" placeholder="Дата начала">
    <input v-model="end_date" class="styled-input" type="date" placeholder="Дата завершения (необязательно)">
    <button class="styled-button" @click="addProjectExecution">
      Добавить исполнение
    </button>
  </div>
</template>

<style scoped>
.styled-input-container {
  text-align: center;
}

.styled-label {
  display: block;
  text-align: center;
  margin: 0 auto 10px;
}

.styled-input {
  display: block;
  width: auto;
  margin: 0 auto 10px;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
}

.styled-button {
  display: inline-block;
  padding: 10px 20px;
  font-size: 16px;
  text-align: center;
  border: 1px solid #ccc;
  cursor: pointer;
}
</style>
