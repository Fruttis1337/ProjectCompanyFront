<script setup lang="ts">
import { ref } from 'vue'

const employees = ref(null)
const projectId = ref('')

async function getEmployees() {
  try {
    const response = await fetch(`http://127.0.0.1:8000/project/employees?project_id=${projectId.value}`)
    if (response.ok) {
      const data = await response.json()
      employees.value = data
    }
    else {
      console.error('Ошибка при получении участников проекта:', response.statusText)
    }
  }
  catch (error) {
    console.error('Ошибка при получении участников проекта:', error)
  }
}
</script>

<template>
  <div>
    <h2>Список участников проекта</h2>
    <label for="projectId">ID проекта:</label>
    <input id="projectId" v-model="projectId" type="text" class="styled-input">
    <button class="styled-button" @click="getEmployees">
      Получить участников проекта
    </button>
    <div v-if="employees !== null">
      <ul>
        <li v-for="employee in employees" :key="employee.id">
          <p>Имя: {{ employee.name }}</p>
          <p>Фамилия: {{ employee.lastname }}</p>
          <p>Должность: {{ employee.position }}</p>
          <p>Категория: {{ employee.category }}</p>
          <p>Отдел: {{ employee.department_name }}</p>
          <p>Дата рождения: {{ employee.birthday }}</p>
          <p>Email: {{ employee.mail }}</p>
          <p>ID: {{ employee.id }}</p>
        </li>
      </ul>
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
