<script setup lang="ts">
function onGetProjectsInInterval() {

}
function onPostProjectExec() {

}
function onFinishProject() {

}
function onCreateProjects() {

}
</script>

<template>
  <div class="button-container">
    <button class="action-button" @click="onGetProjectsInInterval">
      Получить информацию о проектах за указаный промежуток
    </button>
    <button class="action-button" @click="onPostProjectExec">
      Задать сроки проекта
    </button>
    <button class="action-button" @click="onCreateProjects">
      Создать проекты
    </button>
    <button class="action-button" @click="onFinishProject">
      Завершить проект
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
