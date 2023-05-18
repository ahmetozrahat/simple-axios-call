<template>
  <div class="container py-5">
    <h1 class="text-center">To-Do List</h1>
    <div class="row">
      <div class="col-md-6 offset-md-3">
        <div class="card">
          <div class="card-header">
            Listeler
          </div>
          <div class="card-body">
            <ul v-if="todoIsLoading == false" class="list-group">
              <li v-for="(todo, index) in todos" :key="index" class="list-group-item">
                {{ todo.title }}
              </li>
            </ul>
            <h5 v-else>Yükleniyor...</h5>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: "App",
  data() {
    return {
      url: "https://jsonplaceholder.typicode.com/todos",
      todos: [],
      todoIsLoading: true
    };
  },
  created() {
    axios.get(this.url)
    .then(response => (this.todos = response.data))
    .finally(() => (this.todoIsLoading = false))
    .catch((error) => console.log(error));
  }
}

</script>