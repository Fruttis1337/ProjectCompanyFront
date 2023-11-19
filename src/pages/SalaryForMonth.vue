<script setup lang="ts">
import { ref } from 'vue'

const salaryResult = ref(null)

async function computeSalary() {
  try {
    const response = await fetch('http://127.0.0.1:8000/contract/salary')
    if (response.ok) {
      const data = await response.json()
      salaryResult.value = data
    }
    else {
      console.error('Ошибка при получении заработной платы:', response.statusText)
    }
  }
  catch (error) {
    console.error('Ошибка при получении заработной платы:', error)
  }
}
</script>

<template>
  <div>
    <h2>Расчет стоимости контрактов</h2>
    <button class="styled-button" @click="computeSalary">
      Рассчитать стоимость
    </button>
    <div v-if="salaryResult !== null">
      <p>Общая стоимость контрактов за последние 30 дней: {{ salaryResult.price }} руб.</p>
    </div>
  </div>
</template>

<style scoped>
.styled-button {
  padding: 10px 20px;
  font-size: 16px;
  text-align: center;
  border: 1px solid #000;
}
</style>
