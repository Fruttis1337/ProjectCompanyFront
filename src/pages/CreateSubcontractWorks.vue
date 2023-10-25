<script setup>
import { ref } from 'vue'
import axios from 'axios'

const subcontractorWorksData = ref([
  {
    subcontractor_id: null,
    project_id: null,
    start_date: null,
    end_date: null,
    price: null,
  },
])

async function addSubcontractorWorks() {
  try {
    await axios.post('http://127.0.0.1:8000/subcontractor-works/', subcontractorWorksData.value)
    // Обработка ответа, если необходимо
  }
  catch (error) {
    console.error('Ошибка при добавлении работ субподрядчика', error)
  }
}
</script>

<template>
  <h2>Добавить работы субподрядчика</h2>
  <form class="centered-form" @submit.prevent="addSubcontractorWorks">
    <div v-for="(work, index) in subcontractorWorksData" :key="index">
      <h3>Работа {{ index + 1 }}</h3>
      <div class="form-group">
        <label for="subcontractor_id">ID субподрядчика:</label>
        <input id="subcontractor_id" v-model="work.subcontractor_id" type="number" required class="input-field">
      </div>
      <div class="form-group">
        <label for="project_id">ID проекта:</label>
        <input id="project_id" v-model="work.project_id" type="number" required class="input-field">
      </div>
      <div class="form-group">
        <label for="start_date">Дата начала работы:</label>
        <input id="start_date" v-model="work.start_date" type="date" required class="input-field">
      </div>
      <div class="form-group">
        <label for="end_date">Дата окончания работы:</label>
        <input id="end_date" v-model="work.end_date" type="date" class="input-field">
      </div>
      <div class="form-group">
        <label for="price">Стоимость:</label>
        <input id="price" v-model="work.price" type="number" required class="input-field">
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
