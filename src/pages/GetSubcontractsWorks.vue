<script setup>
import { onMounted, ref } from 'vue'
import axios from 'axios'

const subcontractorWorks = ref([])

async function fetchSubcontractorWorks() {
  try {
    const response = await axios.get('http://127.0.0.1:8000/subcontractor_works/')
    subcontractorWorks.value = response.data
  }
  catch (error) {
    console.error('Ошибка при получении данных о работах подрядчика', error)
  }
}

onMounted(() => {
  fetchSubcontractorWorks()
})
</script>

<template>
  <div class="subcontractor-works">
    <h2>Работы подрядчика</h2>
    <table>
      <thead>
        <tr>
          <th>Название подрядчика</th>
          <th>Название работы</th>
          <th>Общая стоимость</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(work, index) in subcontractorWorks" :key="index">
          <td>{{ work.title }}</td>
          <td>{{ work.WorksSubcontracts.title }}</td>
          <td>{{ work.total_price }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>
.subcontractor-works {
  text-align: center;
  margin: 20px;
}

table {
  width: 100%;
  border-collapse: collapse;
}

table th,
table td {
  border: 1px solid #ccc;
  padding: 8px;
  text-align: left;
}

thead {
  background-color: #f2f2f2;
}
</style>
