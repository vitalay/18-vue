<template>
    <div>
      <div v-if="people.length === 0">Список пуст</div>
      <div class="card" v-for="person in people" :key="person.id">
        <h3>{{ person.firstName }}</h3>
        <button class="btn-danger" @click="$emit('remove', person.id)">Удалить</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      people: {
        type: Array,
        required: true,
      },
    },
  };
  </script>
  
  <style scoped>
  .card {
    padding: 1rem;
    margin: 0.5rem 0;
    border: 1px solid #ddd;
    border-radius: 4px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  
  .btn-danger {
    background-color: #e74c3c;
    color: #fff;
    border: none;
    padding: 0.5rem 1rem;
    cursor: pointer;
    border-radius: 4px;
  }
  
  .btn-danger:hover {
    background-color: #c0392b;
  }
  </style>
  