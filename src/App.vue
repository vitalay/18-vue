<template>
  <div class="container">
    <form class="card">
      <h2>Работа с базой данных</h2>

      <div class="form-control">
        <label for="name"> Имя </label>
        <input type="text" id="name" v-model.trim="name" placeholder="Введите имя">
      </div>

      <button class="btn-primary" :disabled="name.length === 0">Создать человека</button>

    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: ''
    }
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
  background-color: #9e20009d;
  color: white;
  border: none;
  padding: 0.5rem 1rem;
  border-radius: 4px;
  cursor: pointer;
}

.btn-primary:hover {
  background-color: #0056b3;
}
</style>