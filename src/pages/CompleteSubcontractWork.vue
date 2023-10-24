<script setup>
import { ref } from 'vue'
import axios from 'axios'

const project_id = ref(null)
const subcontractor_id = ref(null)
const work_id = ref(null)
const end_date = ref(null)

async function completeWork() {
  try {
    const response = await axios.patch(`/complete-subcontractor-work/${project_id.value}/${subcontractor_id.value}/${work_id.value}/`, {
      end_date: end_date.value,
    })
    // eslint-disable-next-line no-console
    console.log('Работа завершена', response.data)
  }
  catch (error) {
    console.error('Ошибка при завершении работы', error)
  }
}
</script>

<template>
  <div class="complete-subcontractor-work">
    <h2>Завершить работу субподрядчика</h2>
    <form class="form" @submit.prevent="completeWork">
      <label for="project_id">ID проекта:</label>
      <input id="project_id" v-model="project_id" type="number" required class="input-field">
      <label for="subcontractor_id">ID субподрядчика:</label>
      <input id="subcontractor_id" v-model="subcontractor_id" type="number" required class="input-field">
      <label for="work_id">ID работы:</label>
      <input id="work_id" v-model="work_id" type="number" required class="input-field">
      <label for="end_date">Дата окончания работы:</label>
      <input id="end_date" v-model="end_date" type="date" required class="input-field">
      <button type="submit" class="action-button">
        Завершить работу
      </button>
    </form>
  </div>
</template>

<style scoped>
.complete-subcontractor-work {
  text-align: center;
  margin: 20px;
}

.input-field {
  width: auto;
  padding: 10px;
  margin-bottom: 15px;
  font-size: 16px;
  border: 1px solid #ccc;
}

.action-button {
  padding: 10px 20px;
  font-size: 16px;
  text-align: center;
  border: 1px solid #000;
}

.form {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>
