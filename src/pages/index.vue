<script setup lang="ts">
defineOptions({
  name: 'IndexPage',
})

const router = useRouter()

function navigateToDogovora() {
  router.push(`/Dogovor`)
}

function navigateToProjects() {
  router.push(`/Projects`)
}

function navigateToEmployers() {
  router.push(`/Employers`)
}

function navigateToSubcontracts() {
  router.push(`/Subcontracts`)
}
</script>

<template>
  <div class="centered-buttons">
    <button class="bordered-button" @click="navigateToDogovora">
      Договора
    </button>
    <button class="bordered-button" @click="navigateToProjects">
      Проекты
    </button>
    <button class="bordered-button" @click="navigateToEmployers">
      Сотрудники
    </button>
    <button class="bordered-button" @click="navigateToSubcontracts">
      Субподрядчики
    </button>
  </div>
</template>

<route lang="yaml">
meta:
layout: home
</route>

<style scoped>
.centered-buttons {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.bordered-button {
  margin: 5px 0;
  padding: 10px 20px;
  font-size: 16px;
  width: 200px;
  text-align: center;
  border: 1px solid #000; /* Добавление границы вокруг кнопок */
}
</style>
