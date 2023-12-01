<script setup>
import { ref } from 'vue'
import axios from 'axios'

const employeeData = ref({
  name: '',
  lastname: '',
  position: '',
  category: 'constructor',
  department_id: null,
  birthday: '',
  mail: '',
})

const dateOfHire = ref('')
const newEmployeeData = ref(null)

async function addEmployee() {
  try {
    const response = await axios.post(`http://127.0.0.1:8000/add_employee/`, employeeData.value, {
      params: {
        date_of_hire: dateOfHire.value,
      },
    })
    newEmployeeData.value = response.data
  }
  catch (error) {
    console.error('Ошибка при добавлении сотрудника', error)
  }
}
</script>

<template>
  <div class="add-employee">
    <h2>Добавить нового сотрудника</h2>
    <form class="form" @submit.prevent="addEmployee">
      <div class="input-field">
        <label for="name">Имя:</label>
        <input id="name" v-model="employeeData.name" type="text" required>
      </div>
      <div class="input-field">
        <label for="lastname">Фамилия:</label>
        <input id="lastname" v-model="employeeData.lastname" type="text" required>
      </div>
      <div class="input-field">
        <label for="position">Должность:</label>
        <input id="position" v-model="employeeData.position" type="text" required>
      </div>
      <div class="input-field">
        <label for="category">Категория:</label>
        <select id="category" v-model="employeeData.category" required>
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
      <div class="input-field">
        <label for="department_id">ID отдела:</label>
        <input id="department_id" v-model="employeeData.department_id" type="number" required>
      </div>
      <div class="input-field">
        <label for="birthday">Дата рождения:</label>
        <input id="birthday" v-model="employeeData.birthday" type="date" required>
      </div>
      <div class="input-field">
        <label for="mail">Email:</label>
        <input id="mail" v-model="employeeData.mail" type="email" required>
      </div>
      <div class="input-field">
        <label for="dateOfHire">Дата найма:</label>
        <input id="dateOfHire" v-model="dateOfHire" type="date" required>
      </div>
      <button type="submit" class="submit-button">
        Добавить сотрудника
      </button>
    </form>
    <div v-if="newEmployeeData">
      <h3>Новый сотрудник добавлен:</h3>
      <pre> {{ newEmployeeData.name }} {{ newEmployeeData.lastname }} ID:{{ newEmployeeData.id }}</pre>
    </div>
  </div>
</template>

<style scoped>
.add-employee {
  text-align: center;
  margin: 20px;
}

.input-field {
  display: flow;
  flex-direction: column;
  align-items: center;
  width: fit-content;
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

.form {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
