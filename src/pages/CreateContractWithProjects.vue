<script setup>
import { ref } from 'vue'
import axios from 'axios'

const contractData = ref({
  title: '',
  client: '',
  price: 0,
})
const projectIds = ref('')

async function createContractWithProjects() {
  try {
    const projectIdsArray = projectIds.value.split(',').map(id => Number.parseInt(id.trim()))
    const requestBody = {
      contract_data: contractData,
      project_ids: projectIdsArray,
    }

    // Выполнить запрос к серверу
    const response = await axios.post('http://127.0.0.1:8000/create_contract_with_projects/', requestBody)
    // eslint-disable-next-line no-console
    console.log(response.data) // Печать ответа сервера
  }
  catch (error) {
    console.error('Ошибка:', error)
  }
}
</script>

<template>
  <div>
    <h2>Создать договор и назначить его проекты</h2>
    <div class="input-container">
      <label for="contractTitle" class="styled-label">Название договора:</label>
      <input id="contractTitle" v-model="contractData.title" type="text" class="styled-input">
    </div>
    <div class="input-container">
      <label for="contractClient" class="styled-label">Клиент:</label>
      <input id="contractClient" v-model="contractData.client" type="text" class="styled-input">
    </div>
    <div class="input-container">
      <label for="contractPrice" class="styled-label">Стоимость:</label>
      <input id="contractPrice" v-model="contractData.price" type="number" class="styled-input">
    </div>
    <div class="input-container">
      <label for="projectIds" class="styled-label">Проекты (ID, через запятую):</label>
      <input id="projectIds" v-model="projectIds" type="text" class="styled-input">
    </div>
    <button class="styled-button" @click="createContractWithProjects">
      Создать договор
    </button>
  </div>
</template>

<style scoped>
.styled-input-container {
  text-align: center; /* Центрируем содержимое по горизонтали */
}

.styled-input {
  display: block; /* Делаем элементы ввода блочными, чтобы выровнять их по центру */
  width: auto; /* Определяем ширину элементов ввода автоматически */
  margin: 0 auto 10px; /* Центрируем элементы ввода, добавляем небольшое расстояние снизу */
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
}

.styled-label {
  display: block;
  text-align: center; /* Центрируем текст метки */
  margin: 0 auto 10px; /* Центрируем метку и добавляем небольшое расстояние снизу */
}

.styled-button-container {
  text-align: center; /* Центрируем кнопку по горизонтали */
}

.styled-button {
  display: inline-block; /* Делаем кнопку инлайновой */
  padding: 10px 20px;
  font-size: 16px;
  text-align: center;
  border: 1px solid #ccc;
  cursor: pointer;
}
</style>
