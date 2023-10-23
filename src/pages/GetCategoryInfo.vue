<script setup>
import { ref } from 'vue'
import axios from 'axios'

const category = ref('')
const startDate = ref('')
const endDate = ref('')
const participationInfo = ref([])

async function getCategoryParticipationInfo() {
  try {
    const response = await axios.get(`/category_participation_info/?category=${category.value}&start_date=${startDate.value}&end_date=${endDate.value}`)
    participationInfo.value = response.data
  }
  catch (error) {
    console.error('Ошибка при получении информации', error)
  }
}
</script>

<template>
  <div class="participation-info-container">
    <h2>Информация о участии в проектах</h2>
    <form class="participation-form" @submit.prevent="getCategoryParticipationInfo">
      <div class="input-group">
        <label for="category" class="input-label">Категория:</label>
        <select id="category" v-model="category" class="input-field" required>
          <option value="constructor">
            Конструктор
          </option>
          <option value="engineer">
            Инженер
          </option>
          <option value="technician">
            Техник
          </option>
          <option value="lab_assistant">
            Лаборант
          </option>
          <option value="service_staff">
            Обслуживающий персонал
          </option>
        </select>
      </div>

      <div class="input-group">
        <label for="start_date" class="input-label">Начальная дата:</label>
        <input id="start_date" v-model="startDate" type="date" class="input-field" required>
      </div>

      <div class="input-group">
        <label for="end_date" class="input-label">Конечная дата:</label>
        <input id="end_date" v-model="endDate" type="date" class="input-field" required>
      </div>

      <button class="action-button">
        Получить информацию
      </button>
    </form>

    <div v-if="participationInfo.length > 0">
      <h3 class="info-header">
        Информация о участии в проектах:
      </h3>
      <ul class="employee-list">
        <li v-for="info in participationInfo" :key="info.employee.id" class="employee-item">
          <strong class="employee-name">{{ info.employee.name }} {{ info.employee.lastname }}</strong>
          <ul class="project-list">
            <li v-for="project in info.projects_participation" :key="project.id" class="project-item">
              {{ project.title }}
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.participation-info-container {
  text-align: center;
  margin: 20px;
}

.participation-form {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  margin-bottom: 20px;
}

.input-group {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 5px;
}

.input-label {
  font-weight: bold;
}

.input-field {
  width: auto;
  padding: 8px;
  font-size: 16px;
  border: 1px solid #ccc;
}

.action-button {
  padding: 10px 20px;
  font-size: 16px;
  text-align: center;
  border: 1px solid #000;
}

.info-header {
  font-size: 18px;
  font-weight: bold;
}

.employee-list {
  list-style: none;
  padding: 0;
}

.employee-item {
  margin: 10px 0;
}

.employee-name {
  font-weight: bold;
}

.project-list {
  list-style: disc;
  padding-left: 20px;
}

.project-item {
  margin: 5px 0;
}
</style>
