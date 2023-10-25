<script setup lang="ts">
const router = useRouter()
function onGetEquipmentDistr() {
  router.push('/GetEquipmentDistr')
}
function onGetEquipmentUsageByProject() {
  router.push('/GetEquipmentDistrProj')
}
function onBindEquipment() {

}
function onCreateEquipment() {

}
</script>

<template>
  <div class="button-container">
    <button class="action-button" @click="onGetEquipmentDistr">
      Получить информацию о распределении оборудавания на указанную дату
    </button>
    <button class="action-button" @click="onGetEquipmentUsageByProject">
      Получить информацию о использовании оборудования указанным проектом
    </button>
    <button class="action-button" @click="onBindEquipment">
      Назначить оборудование
    </button>
    <button class="action-button" @click="onCreateEquipment">
      Создать оборудование
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
