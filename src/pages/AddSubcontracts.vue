<script setup>
import { ref } from 'vue'
import axios from 'axios'

const subcontractorData = ref([
  {
    title: '',
    description: '',
  },
])

async function addSubcontractors() {
  try {
    await axios.post('/subcontractors/', subcontractorData.value)
    // Обработка ответа, если необходимо
  }
  catch (error) {
    console.error('Ошибка при добавлении подрядчиков', error)
  }
}
</script>

<template>
  <h2>Добавить подрядчиков</h2>
  <form class="centered-form" @submit.prevent="addSubcontractors">
    <div v-for="(subcontractor, index) in subcontractorData" :key="index">
      <h3>Подрядчик {{ index + 1 }}</h3>
      <div class="form-group">
        <label for="title">Название подрядчика:</label>
        <input id="title" v-model="subcontractor.title" type="text" required class="input-field">
      </div>
      <div class="form-group">
        <label for="description">Описание подрядчика:</label>
        <textarea id="description" v-model="subcontractor.description" rows="4" class="input-field" />
      </div>
      <hr>
      <button type="submit" class="action-button">
        Добавить подрядчиков
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
  width: 100%;
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
