<script>
  import List from './components/List.vue'
  export default {
    components: { List },
    data() {
      return {
        todo: '',
        todos: []
      }
    },
    mounted() {
      if(localStorage.getItem('todos') !== null)
        this.todos = JSON.parse(localStorage.getItem('todos'))
    },
    computed: {
      totalTodo() {
        if(this.todos != null)
          return this.todos.length;
      }
    },
    methods: {
      add() {
        this.todos.unshift({
          activity: this.todo,
          isDone: false
        });
        this.todo = '';
        this.saveToLocalStorage();
      },
      deleteTodo(todoIndex) {
        this.todos = this.todos.filter((item, index) => {
          if (index != todoIndex) {
            return item
          }
        });
        this.saveToLocalStorage();
      },
      doneTodo(todoIndex) {
        this.todos = this.todos.filter((item, index) => {
          if (index == todoIndex) {
            return item.isDone = true
          }

          return item
        });
        this.saveToLocalStorage();
      },
      saveToLocalStorage() {
        localStorage.setItem('todos', JSON.stringify(this.todos))
      }
    }
  }
</script>

<template>
  <div class="container" style="margin-top: 20px">
    <div class="card">
      <div class="card-header">
        <h5 class="card-title">Simple Todo App</h5>
      </div>
      <div class="card-body">
        <div class="row mb-2">
          <div class="col-10">
            <input v-model="todo" @keyup.enter="add" type="text" name="" id="" class="form-control">
          </div>
          <div class="col-2">
            <button @click="add" class="btn btn-success">Add</button>
          </div>
        </div>
        <list :todos="todos" @doneTodo="doneTodo" @deleteTodo="deleteTodo"/>
        <small>Total Todo: {{ totalTodo }}</small>
      </div>
    </div>
  </div>
</template>

<style>

</style>