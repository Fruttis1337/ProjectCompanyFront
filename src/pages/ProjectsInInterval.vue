<script setup>
import { ref } from 'vue'
import axios from 'axios'

const startDate = ref('')
const endDate = ref('')
const projects = ref([])

async function getProjectsInInterval() {
  try {
    // Выполнить запрос к серверу, передав начальную и конечную дату
    const response = await axios.get(`http://127.0.0.1:8000/projects_in_interval/?start_date=${startDate.value}&end_date=${endDate.value}`)
    projects.value = response.data // Обновить список проектов
  }
  catch (error) {
    console.error('Ошибка:', error)
  }
}
</script>

<template>
  <div>
    <h2>Проекты в интервале дат</h2>
    <div class="input-container">
      <label for="startDate" class="styled-label">Начальная дата:</label>
      <input id="startDate" v-model="startDate" type="date" class="styled-input">
    </div>
    <div class="input-container">
      <label for="endDate" class="styled-label">Конечная дата:</label>
      <input id="endDate" v-model="endDate" type="date" class="styled-input">
    </div>
    <button class="styled-button" @click="getProjectsInInterval">
      Получить проекты
    </button>
    <table class="styled-table">
      <thead>
        <tr>
          <th>ID</th>
          <th>Название</th>
          <th>Идентификатор менеджера</th>
          <th>Договор</th>
          <!-- Добавьте другие заголовки столбцов по вашим потребностям -->
        </tr>
      </thead>
      <tbody>
        <tr v-for="project in projects" :key="project.id">
          <td>{{ project.id }}</td>
          <td>{{ project.title }}</td>
          <td>{{ project.manager_id }}</td>
          <td>{{ project.contract_id }}</td>
          <!-- Вывод других полей проекта по вашим потребностям -->
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
.styled-table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 20px;
}

.styled-table th,
.styled-table td {
  padding: 8px 12px;
  border: 1px solid #ccc;
  text-align: left;
}

.styled-table th {
  background-color: #f2f2f2;
  font-weight: bold;
}

.styled-table tbody tr:nth-child(even) {
  background-color: #f5f5f5;
}

.styled-table tbody tr:hover {
  background-color: #e0e0e0;
}

.styled-label {
  margin-right: 10px;
}

.styled-input {
  display: block;
  width: auto;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  margin: 0 auto;
}

.styled-button {
  display: inline-block;
  margin-top: 10px;
  padding: 10px 20px;
  font-size: 16px;
  text-align: center;
  border: 1px solid #ccc;
  background-color: #007BFF;
  color: #fff;
  cursor: pointer;
}

.styled-button:hover {
  background-color: #0056b3;
}
</style>
