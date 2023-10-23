<script setup lang="ts">
const router = useRouter()
function onGetProjectsInContract() {
  router.push('/ProjectsInContract')
}
function onGetContractForProject() {
  router.push('/ContractsByProjects')
}
function onGetContractCosts() {
  router.push('/ContractCostsInInterval')
}
function onCreateContractWithProjects() {
  router.push('/CreateContractWithProjects')
}
</script>

<template>
  <div class="button-container">
    <button class="action-button" @click="onGetProjectsInContract">
      Получить информацию о проектах в договоре
    </button>
    <button class="action-button" @click="onGetContractForProject">
      Получить информацию о договорах по проектам
    </button>
    <button class="action-button" @click="onGetContractCosts">
      Получить стоимость выполненных договоров
    </button>
    <button class="action-button" @click="onCreateContractWithProjects">
      Создать договор и назначить его проекты
    </button>
  </div>
</template>

<style scoped>
.button-container {
  display: flex;
  flex-direction: column;
  align-items: center; /* Горизонтальное центрирование */
}

.action-button {
  margin: 10px 0; /* Расстояние между кнопками */
  padding: 10px 20px;
  font-size: 16px;
  text-align: center;
  border: 1px solid #000; /* Добавление границы вокруг кнопок */
}
</style>
