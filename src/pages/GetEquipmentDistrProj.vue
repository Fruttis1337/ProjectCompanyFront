<script setup>
import { ref } from 'vue'
import axios from 'axios'

const projectID = ref(null)
const equipmentUsage = ref([])

async function getEquipmentUsageByProject() {
  try {
    const response = await axios.get(`http://127.0.0.1:8000/equipment_usage_by_project/?project_id=${projectID.value}`)
    equipmentUsage.value = response.data
  }
  catch (error) {
    console.error('Ошибка при получении информации об использовании оборудования в проекте', error)
  }
}
</script>

<template>
  <h2>Использование оборудования в проекте</h2>
  <div class="centered-form">
    <div class="form-group">
      <label for="projectID">ID проекта:</label>
      <input id="projectID" v-model="projectID" type="number" class="input-field">
      <button class="action-button" @click="getEquipmentUsageByProject">
        Получить использование оборудования
      </button>
    </div>
    <div v-if="equipmentUsage.length > 0">
      <h3>Использование оборудования в проекте (ID проекта: {{ projectID }})</h3>
      <table>
        <thead>
          <tr>
            <th>Наименование оборудования</th>
            <th>Дата начала распределения</th>
            <th>Дата окончания распределения</th>
          <!-- Другие заголовки таблицы -->
          </tr>
        </thead>
        <tbody>
          <tr v-for="(equipment, index) in equipmentUsage" :key="index">
            <td>{{ equipment.title }}</td>
            <td>{{ equipment.data_start_distr }}</td>
            <td>{{ equipment.date_end_distr }}</td>
          <!-- Вывод других данных об использовании оборудования -->
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<style scoped>
.centered-form {
  display: flex;
  justify-content: center;
  align-items: center;
}

.form-group {
  margin-bottom: 20px;
}

.input-field {
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
}

.action-button {
  padding: 10px 20px;
  font-size: 16px;
  text-align: center;
  border: 1px solid #000;
}

table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #ccc;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}
</style>
