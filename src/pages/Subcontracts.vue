<script setup lang="ts">
function onGetProjectsInContract() {

}
function onGetContractForProject() {

}
function onGetContractCosts() {

}
function onCreateContract() {

}
</script>

<template>
  <div class="button-container">
    <button class="action-button" @click="onGetProjectsInContract">
      Получить информацию о проектах в договоре
    </button>
    <button class="action-button" @click="onGetContractForProject">
      Получить информацию о договоре для проекта
    </button>
    <button class="action-button" @click="onGetContractCosts">
      Получить стоимость выполненных договоров
    </button>
    <button class="action-button" @click="onCreateContract">
      Создать договор
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
