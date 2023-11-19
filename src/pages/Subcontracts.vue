<script setup lang="ts">
const router = useRouter()
function onGetSubcontractsWorks() {
  router.push('/GetSubcontractsWorks')
}
function onCreateSubcontractorWorks() {
  router.push('/CreateSubcontractWorks')
}
function onCreateSubcontractors() {
  router.push('/AddSubcontracts')
}
</script>

<template>
  <div class="button-container">
    <button class="action-button" @click="onGetSubcontractsWorks">
      Получить информацию о стоимости работ субподрядчиков
    </button>
    <button class="action-button" @click="onCreateSubcontractorWorks">
      Назначить работы субподрядчику
    </button>
    <button class="action-button" @click="onCreateSubcontractors">
      Создать субподрядчиков
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
