<template>
  <div class="container">
    <form class="card" @submit.prevent="createPerson">
      <h2>Работа с базой данных</h2>

      <div class="form-control">
        <label for="name"> Имя </label>
        <input type="text" id="name" v-model.trim="name" placeholder="Введите имя">
      </div>

      <button class="btn-primary" :disabled="name.length === 0">Создать человека</button>

      <app-people-list 
      :people="people"
      @load="loadPeople"
      ></app-people-list>

    </form>
  </div>
</template>

<script>

import AppPeopleList from './AppPeopleList.vue';
import axios from 'axios';
export default {

  data() {
    return {
      name: '',
      people: []
    }
  },
  methods: {
    async loadPeople() {
      const {data} = await axios.get('https://vue-90fbd-default-rtdb.firebaseio.com/people.json')
     const result = Object.keys(data).map(key => {
  return {
    id: key,
   ...data[key]
  }

})
  this.people =result

    },
   async  createPerson() {
  
    const response = await fetch('https://vue-90fbd-default-rtdb.firebaseio.com/people.json',  {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify( { 
          firstName: this.name
        })

      })
const firebasaData = await response.json()
console.log(firebasaData) 
this.name = ''

    }
  },
  components: {
    AppPeopleList
  } 
}
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