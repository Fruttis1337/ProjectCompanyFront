<script setup>
import { ref } from 'vue'
import axios from 'axios'

const projectId = ref(null)

const employeesData = ref([
  {
    employee_id: null, // Поле для ID сотрудника
    start_work: null, // Поле для даты начала работы
    end_work: null, // Поле для даты окончания работы
    // Другие поля для данных о сотруднике
  },
])

const addedEmployees = ref([])

async function addEmployeesToProject() {
  try {
    const data = {
      project_id: projectId.value,
      employees_data: employeesData.value,
    }

    const response = await axios.post('/add_employees_to_project/', data)
    addedEmployees.value = response.data
  }
  catch (error) {
    console.error('Ошибка при добавлении сотрудников к проекту', error)
  }
}
</script>

<template>
  <div class="add-employees">
    <h2>Добавить сотрудников к проекту</h2>
    <form class="form" @submit.prevent="addEmployeesToProject">
      <label for="projectId">ID проекта:</label>
      <input id="projectId" v-model="projectId" type="number" required class="input-field">
      <div v-for="(employee, index) in employeesData" :key="index" class="employee-section">
        <h3>Сотрудник {{ index + 1 }}</h3>
        <label for="employeeId">ID сотрудника:</label>
        <input id="employeeId" v-model="employee.employee_id" type="number" required class="input-field">
        <label for="startWork">Дата начала работы:</label>
        <input id="startWork" v-model="employee.start_work" type="date" required class="input-field">
        <label for="endWork">Дата окончания работы:</label>
        <input id="endWork" v-model="employee.end_work" type="date" class="input-field">
        <hr>
      </div>
      <button type="submit" class="submit-button">
        Добавить сотрудников к проекту
      </button>
    </form>
    <div v-if="addedEmployees.length > 0" class="added-employees">
      <h2>Добавленные сотрудники</h2>
      <ul>
        <li v-for="(employee, index) in addedEmployees" :key="index" class="added-employee">
          ID сотрудника: {{ employee.employee_id }} (ID проекта: {{ projectId }})
          <!-- Вывод другой информации о сотруднике и его участии в проектах -->
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.add-employees {
  text-align: center;
  margin: 20px;
}

.form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.input-field {
  width: auto;
  margin: 10px;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
}

.submit-button {
  margin: 10px;
  padding: 10px 20px;
  font-size: 16px;
  border: 1px solid #000;
}

.added-employees {
  text-align: center;
  margin: 20px;
}

.added-employee {
  border: 1px solid #ccc;
  padding: 10px;
  margin: 10px;
}

.employee-section {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
