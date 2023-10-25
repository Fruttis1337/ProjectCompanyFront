<script setup>
import { ref } from 'vue'
import axios from 'axios'

const employeeId = ref(null)
const dateOfDismissal = ref(null)

async function dismissEmployee() {
  try {
    const response = await axios.put(`http://127.0.0.1:8000/dismiss_employee/?employee_id=${employeeId.value}&date_of_dismissal=${dateOfDismissal.value}`)
    if (response.data) {
      // eslint-disable-next-line no-alert
      alert('Сотрудник уволен успешно.')
      // Сбросить введенные данные после увольнения
      employeeId.value = null
      dateOfDismissal.value = null
    }
  }
  catch (error) {
    console.error('Ошибка при увольнении сотрудника', error)
    // eslint-disable-next-line no-alert
    alert('Не удалось уволить сотрудника. Проверьте введенные данные и попробуйте снова.')
  }
}
</script>

<template>
  <div class="dismiss-employee">
    <h2>Увольнение сотрудника</h2>
    <form class="form" @submit.prevent="dismissEmployee">
      <div class="input-block">
        <label for="employeeId">ID сотрудника:</label>
        <input id="employeeId" v-model="employeeId" type="number" required>
      </div>
      <div class="input-block">
        <label for="dateOfDismissal">Дата увольнения:</label>
        <input id="dateOfDismissal" v-model="dateOfDismissal" type="date" required>
      </div>
      <div class="button-container">
        <button type="submit" class="submit-button">
          Уволить сотрудника
        </button>
      </div>
    </form>
  </div>
</template>

<style scoped>
.dismiss-employee {
  text-align: center;
  margin: 20px;
}

.form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.input-block {
  display: flow;
  flex-direction: column;
  align-items: center;
  width: fit-content;
  margin: 10px;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
}

.button-container {
  grid-column: span 2;
  text-align: center;
}

.submit-button {
  margin: 10px;
  padding: 10px 20px;
  font-size: 16px;
  border: 1px solid #000;
}
</style>
