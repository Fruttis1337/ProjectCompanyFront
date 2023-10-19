<script setup lang="ts">
import { ref } from 'vue'
import axios from 'axios'

const projectIds = ref('')
const contracts = ref([])

async function getContractsByProjects() {
  try {
    const projectIdsArray = projectIds.value.split(',').map(Number)
    // Выполните запрос к API для получения контрактов по проектам
    const response = await axios.get('/contracts_by_projects/', {
      params: {
        projectIds: projectIdsArray,
      },
    })

    // Обновите contracts с данными из ответа
    contracts.value = response.data
  }
  catch (error) {
    console.error('Ошибка при запросе контрактов по проектам:', error)
  }
}
</script>

<template>
  <div>
    <h1>Договоры по проектам</h1>
    <div class="input-container">
      <label for="projectIdsInput">Введите ID проектов (через запятую):</label>
      <input id="projectIdsInput" v-model="projectIds" type="text" class="input-block">
      <button class="action-button" @click="getContractsByProjects">
        Получить договоры
      </button>
    </div>
    <table v-if="contracts.length">
      <thead>
        <tr>
          <th>ID</th>
          <th>Название</th>
          <th>Клиент</th>
          <th>Цена</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="contract in contracts" :key="contract.id">
          <td>{{ contract.id }}</td>
          <td>{{ contract.title }}</td>
          <td>{{ contract.client }}</td>
          <td>{{ contract.price }}</td>
        </tr>
      </tbody>
    </table>
    <div v-else>
      <p>Введите ID проектов (через запятую) и нажмите "Получить договоры"</p>
    </div>
  </div>
</template>

<style scoped>
.input-container {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

input {
  margin-right: 10px;
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

.input-block {
  display: block; /* Сделать input блочным элементом */
  width: auto; /* Заполнить всю доступную ширину контейнера */
  margin-right: 25px;
  padding: 10px 10px 10px 10px;
  font-size: 16px;
  border: 1px solid #ccc; /* Граница вокруг input */
}

.action-button {
  padding: 10px 20px;
  font-size: 16px;
  border: 1px solid #000;
}
</style>
