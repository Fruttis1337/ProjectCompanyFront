<script>
export default {
  data() {
    return {
      contractId: '',
      projects: [],
    }
  },
  methods: {
    async getProjectsInContract() {
      // Отправляем запрос на сервер для получения проектов по contract_id
      try {
        const response = await fetch(`http://127.0.0.1:8000/projects_in_contract/${this.contractId}/`)
        if (response.ok) {
          const data = await response.json()
          this.projects = data // Обновляем список проектов
        }
        else {
          // Обработка ошибки, например, вывод сообщения пользователю
          console.error('Ошибка при получении проектов.')
        }
      }
      catch (error) {
        console.error('Ошибка при выполнении запроса: ', error)
      }
    },
  },
}
</script>

<template>
  <div>
    <h1>Информация о проектах в договоре</h1>
    <div class="input-container">
      <label for="contractIdInput">Введите ID договора:</label>
      <input id="contractIdInput" v-model="contractId" class="input-block" type="text">
      <button class="action-button" @click="getProjectsInContract">
        Получить проекты
      </button>
    </div>
    <table v-if="projects.length">
      <thead>
        <tr>
          <th>ID</th>
          <th>Название проекта</th>
          <th>Менеджер</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="project in projects" :key="project.id">
          <td>{{ project.id }}</td>
          <td>{{ project.title }}</td>
          <td>{{ project.manager_id }}</td>
        </tr>
      </tbody>
    </table>
    <div v-else>
      <p>Нет проектов</p>
    </div>
  </div>
</template>

<style scoped>
.input-container {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.input-block {
  display: block;
  width: auto;
  margin-right: 10px;
  padding: 10px;
  font-size: 16px;
  border: 1px solid #ccc;
}

.button-container {
  display: block; /* Сделать кнопку блочным элементом */
  text-align: center; /* Выравнивание текста по центру */
  margin-top: 10px; /* Расстояние между инпутом и кнопкой */
}

.action-button {
  padding: 10px 20px;
  font-size: 16px;
  border: 1px solid #000;
}
/* Остальные стили остаются без изменений */
table {
  width: 100%;
  border-collapse: collapse;
}

th, td {
  border: 1px solid #ccc;
  padding: 8px;
  text-align: left;
}

th {
  background-color: #f2f2f2;
}
</style>
