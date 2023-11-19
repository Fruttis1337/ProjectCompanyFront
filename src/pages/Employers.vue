<script setup lang="ts">
const router = useRouter()
function onGetCategoryParticipationInfo() {
  router.push('/GetCategoryInfo')
}
function onGetEmployeParticipationInfo() {
  router.push('/GetEmployerInfo')
}
function onPostAddEmploye() {
  router.push('/AddEmployer')
}

function onDeleteEmploye() {
  router.push('/DissmissEmployer')
}
function onPostAddEmployesToProject() {
  router.push('/AddEmployerToProj')
}

function onGetEmplInProject() {
  router.push('/GetEmployeesInProject')
}
</script>

<template>
  <div class="button-container">
    <button class="action-button" @click="onGetCategoryParticipationInfo">
      Получить информацию о участии категорий сотрудников в проектах
    </button>
    <button class="action-button" @click="onGetEmployeParticipationInfo">
      Получить информацию о участии сотрудника в проектах
    </button>
    <button class="action-button" @click="onGetEmplInProject">
      Получить информацию о команде на проекте
    </button>
    <button class="action-button" @click="onPostAddEmployesToProject">
      Добавить сотрудников в проект
    </button>
    <button class="action-button" @click="onPostAddEmploye">
      Нанять сотрудника
    </button>
    <button class="action-button" @click="onDeleteEmploye">
      Уволить сотрудника
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
