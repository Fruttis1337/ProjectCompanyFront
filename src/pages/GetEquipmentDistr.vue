<script setup>
import { ref } from 'vue'
import axios from 'axios'

const projectID = ref(null) // Новое поле для ID проекта
const selectedDate = ref('')

const equipmentDistribution = ref([])

async function getEquipmentDistribution() {
  try {
    const response = await axios.get(`http://127.0.0.1:8000/equipment_distribution/?date=${selectedDate.value}&project_id=${projectID.value}`)
    equipmentDistribution.value = response.data
  }
  catch (error) {
    console.error('Ошибка при получении распределения оборудования', error)
  }
}
</script>

<template>
  <h2>Распределение оборудования</h2>
  <div class="centered-form">
    <div class="form-group">
      <label for="projectID">ID проекта:</label>
      <input id="projectID" v-model="projectID" type="number" class="input-field">
      <label for="distributionDate">Дата распределения:</label>
      <input id="distributionDate" v-model="selectedDate" type="date" class="input-field">
      <button class="action-button" @click="getEquipmentDistribution">
        Получить распределение
      </button>
    </div>
    <div v-if="equipmentDistribution.length > 0">
      <h3>Распределение оборудования на {{ selectedDate }}</h3>
      <table>
        <thead>
          <tr>
            <th>Наименование оборудования</th>
            <th>Дата начала распределения</th>
            <th>Дата окончания распределения</th>
            <th>Проект ID</th> <!-- Новое поле -->
          <!-- Другие заголовки таблицы -->
          </tr>
        </thead>
        <tbody>
          <tr v-for="(equipment, index) in equipmentDistribution" :key="index">
            <td>{{ equipment.title }}</td>
            <td>{{ equipment.data_start_distr }}</td>
            <td>{{ equipment.date_end_distr }}</td>
            <td>{{ equipment.project_id }}</td> <!-- Вывод ID проекта -->
          <!-- Вывод других данных о распределении оборудования -->
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
