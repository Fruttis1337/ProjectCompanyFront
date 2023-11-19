<script setup>
import { ref } from 'vue'
import axios from 'axios'

const subcontractorWorksData = ref([
  {
    subcontracts_id: null,
    project_id: null,
    start_date: '',
    end_date: '',
    price: null,
  },
])

async function addSubcontractorWorks() {
  try {
    // eslint-disable-next-line unused-imports/no-unused-vars
    const response = await axios.post('http://127.0.0.1:8000/subcontractor-works/', subcontractorWorksData.value)
    // Обработка ответа, если необходимо
  }
  catch (error) {
    console.error('Ошибка при добавлении работ субподрядчика', error.text)
  }
}
</script>

<template>
  <h2>Добавить работы субподрядчика</h2>
  <form class="centered-form" @submit.prevent="addSubcontractorWorks">
    <div>
      <div class="form-group">
        <label for="subcontracts_id">ID субподрядчика:</label>
        <input
          id="subcontracts_id" v-model="subcontractorWorksData[0].subcontracts_id" type="number" required
          class="input-field"
        >
      </div>
      <div class="form-group">
        <label for="project_id">ID проекта:</label>
        <input id="project_id" v-model="subcontractorWorksData[0].project_id" type="number" required class="input-field">
      </div>
      <div class="form-group">
        <label for="start_date">Дата начала работы:</label>
        <input id="start_date" v-model="subcontractorWorksData[0].start_date" type="date" required class="input-field">
      </div>
      <div class="form-group">
        <label for="end_date">Дата окончания работы:</label>
        <input id="end_date" v-model="subcontractorWorksData[0].end_date" type="date" class="input-field">
      </div>
      <div class="form-group">
        <label for="price">Стоимость:</label>
        <input id="price" v-model="subcontractorWorksData[0].price" type="number" required class="input-field">
      </div>
      <hr>
      <button type="submit" class="action-button">
        Добавить работы
      </button>
    </div>
  </form>
</template>

<style scoped>
.centered-form {
  display: flex;
  justify-content: center;
  align-items: center;
}

.input-field {
  width: auto;
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
</style>
