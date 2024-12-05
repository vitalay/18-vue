<template>
  <div class="container">
    <form class="card" @submit.prevent="createPerson">
      <h2>Работа с базой данных</h2>

      <div class="form-control">
        <label for="name">Имя</label>
        <input
          type="text"
          id="name"
          v-model.trim="name"
          placeholder="Введите имя"
        />
      </div>

      <button class="btn-primary" :disabled="name.length === 0">
        Создать человека
      </button>

      <!-- Компонент списка -->
      <app-people-list
        :people="people"
        @remove="removePerson"
      ></app-people-list>
    </form>
  </div>
</template>

<script>
import AppPeopleList from "./AppPeopleList.vue";
import axios from "axios";

export default {
  data() {
    return {
      name: "",
      people: [], // Список людей
    };
  },
  mounted() {
    this.loadPeople();
  },
  methods: {
    // Загрузка людей
    async loadPeople() {
  try {
    const { data } = await axios.get('https://vue-90fbd-default-rtdb.firebaseio.com/people.json');
    if (!data) return;

    this.people = Object.values(data).map(person => ({
      id: person.id,
      firstName: person.firstName,
    }));
  } catch (error) {
    console.error('Ошибка при загрузке данных:', error);
  }
},


    // Добавление нового человека
    async createPerson() {
  try {
    const response = await axios.post('https://vue-90fbd-default-rtdb.firebaseio.com/people.json', {
      firstName: this.name,
    });

    // Добавить нового человека в список
    this.people.push({
      id: response.data.name, // ID из Firebase
      firstName: this.name,
    });

    // Очистить поле ввода
    this.name = '';
  } catch (error) {
    console.error('Ошибка при создании человека:', error);
  }
},


    // Удаление человека
    async removePerson(id) {
  try {
    // Сначала удаляем запись из базы данных
    await axios.delete(`https://vue-90fbd-default-rtdb.firebaseio.com/people/${id}.json`);
    
    // Фильтруем список, удаляя элемент с указанным id
    this.people = this.people.filter(person => person.id !== id);
  } catch (error) {
    console.error('Ошибка при удалении человека:', error);
  }
},
  },
  components: {
    AppPeopleList,
  },
};
</script>

<style scoped>
.container {
  max-width: 600px;
  margin: 0 auto;
}

.card {
  background-color: #6d5f5f;
  border: 1px solid #ddd;
  border-radius: 6px;
  padding: 1.5rem;
}

.form-control {
  margin-bottom: 1rem;
}

.form-control.invalid input {
  border-color: #d9534f;
}

.form-control small {
  color: #d9534f;
}

.form-checkbox {
  margin-bottom: 1rem;
}
.btn-primary {
}

.btn-primary:hover {
  background-color: #3a3433;
}
</style>
