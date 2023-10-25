<script setup>
import { ref } from 'vue'
import axios from 'axios'

const employeeId = ref(null)
const startDate = ref('')
const endDate = ref('')
const employeeParticipation = ref(null)

async function getEmployeeParticipationInfo() {
  try {
    const response = await axios.get(`http://127.0.0.1:8000/employee_participation_info/${employeeId.value}/?start_date=${startDate.value}&end_date=${endDate.value}`)
    employeeParticipation.value = response.data
  }
  catch (error) {
    console.error('Ошибка при получении информации о сотруднике', error)
  }
}
</script>

<template>
  <div class="participation-info-container">
    <h2>Информация об участии сотрудника в проектах</h2>
    <form class="participation-form" @submit.prevent="getEmployeeParticipationInfo">
      <div class="input-group">
        <label for="employeeId" class="input-label">ID сотрудника:</label>
        <input id="employeeId" v-model="employeeId" type="number" class="input-field" required>
      </div>

      <div class="input-group">
        <label for="startDate" class="input-label">Дата начала:</label>
        <input id="startDate" v-model="startDate" type="date" class="input-field" required>
      </div>

      <div class="input-group">
        <label for="endDate" class="input-label">Дата окончания:</label>
        <input id="endDate" v-model="endDate" type="date" class="input-field" required>
      </div>

      <button class="action-button">
        Получить информацию
      </button>
    </form>

    <!-- Отображение информации о сотруднике и его участии в проектах -->
    <div v-if="employeeParticipation">
      <h3>Информация о сотруднике:</h3>
      <p><strong>Имя:</strong> {{ employeeParticipation.employee.name }}</p>
      <!-- Другие поля информации о сотруднике -->

      <h3>Участие в проектах:</h3>
      <ul>
        <li v-for="(project, index) in employeeParticipation.projects_participation" :key="index">
          {{ project.title }}
          <!-- Отображение другой информации о проекте -->
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.participation-info-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.participation-form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.input-group {
  margin-bottom: 20px;
}

.input-label {
  font-size: 16px;
  margin-bottom: 5px;
}

.input-field {
  width: auto;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
}

.action-button {
  margin: 10px 0;
  padding: 10px 20px;
  font-size: 16px;
  text-align: center;
  border: 1px solid #000;
}

/* Стили для отображения информации о сотруднике и его участии в проектах */
.employee-info {
  margin-top: 20px;
}

.projects-list {
  list-style: disc;
  margin-left: 20px;
}

.projects-list li {
  margin: 5px 0;
}

/* Остальные стили по необходимости */
</style>
