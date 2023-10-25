<script setup>
import { ref } from 'vue'
import axios from 'axios'

const projectData = ref([
  {
    title: '',
    managerId: null, // Поле для ID менеджера
    // Другие поля для данных о проекте
  },
])

const addedProjects = ref([])

async function addProjects() {
  try {
    const response = await axios.post('http://127.0.0.1:8000/projects/', projectData.value)
    addedProjects.value = response.data
  }
  catch (error) {
    console.error('Ошибка при добавлении проектов', error)
  }
}
</script>

<template>
  <div>
    <h2>Добавить проекты</h2>
    <form @submit.prevent="addProjects">
      <div v-for="(project, index) in projectData" :key="index">
        <h3>Проект {{ index + 1 }}</h3>
        <label for="title">Название проекта:</label>
        <input id="title" v-model="project.title" type="text" required>

        <label for="managerId">ID менеджера:</label>
        <input id="managerId" v-model="project.managerId" type="number" required>

        <!-- Другие поля для ввода данных о проекте -->

        <hr>
      </div>

      <button type="submit">
        Добавить проекты
      </button>
    </form>

    <div v-if="addedProjects.length > 0">
      <h2>Добавленные проекты</h2>
      <ul>
        <li v-for="(project, index) in addedProjects" :key="index">
          <strong>{{ project.title }}</strong> (Менеджер ID: {{ project.managerId }})
          <!-- Вывод других данных о проекте -->
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
h2 {
  font-size: 24px;
  margin-bottom: 10px;
}

form {
  max-width: 400px;
  margin: 0 auto;
}

label {
  display: block;
  font-weight: bold;
  margin-top: 10px;
}

input[type="text"],
input[type="number"] {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-top: 5px;
}

button[type="submit"] {
  display: block;
  width: 100%;
  padding: 10px;
  font-size: 18px;
  background-color: #007BFF;
  color: #fff;
  border: none;
  border-radius: 4px;
  margin-top: 20px;
  cursor: pointer;
}

hr {
  border: 1px solid #ccc;
  margin-top: 20px;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  font-size: 16px;
  margin-bottom: 10px;
}
</style>
