<script setup lang="ts">
import { ref } from 'vue'

const startDate = ref('')
const endDate = ref('')
const totalCost = ref(null)

async function getContractCosts() {
  if (startDate.value && endDate.value) {
    try {
      const response = await fetch(`/contract_costs_in_interval/?start_date=${startDate.value}&end_date=${endDate.value}`)
      if (response.ok) {
        const data = await response.json()
        totalCost.value = data.total_cost
      }
      else {
        console.error('Ошибка при получении стоимости договоров:', response.statusText)
      }
    }
    catch (error) {
      console.error('Ошибка при получении стоимости договоров:', error)
    }
  }
}
</script>

<template>
  <div>
    <h2>Получить стоимость выполненных договоров</h2>
    <div class="input-container">
      <label for="startDate">Начальная дата:</label>
      <input id="startDate" v-model="startDate" type="date" class="styled-input">
    </div>
    <div class="input-container">
      <label for="endDate">Конечная дата:</label>
      <input id="endDate" v-model="endDate" type="date" class="styled-input">
    </div>
    <button class="styled-button" @click="getContractCosts">
      Получить стоимость
    </button>
    <div v-if="totalCost !== null">
      <p>Общая стоимость выполненных договоров в указанный период времени: {{ totalCost }} руб.</p>
    </div>
  </div>
</template>

<style scoped>
.input-container {
  margin-bottom: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.styled-input {
  width: auto;
  padding: 10px;
  margin: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
}

.styled-button {
  padding: 10px 20px;
  font-size: 16px;
  text-align: center;
  border: 1px solid #000;
}
</style>
