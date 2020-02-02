<template>
  <div>
    <h2>Todo</h2>
    <router-link to="/">Home</router-link>
    <hr />
    <AddTodo @add-todo="addTodoHandler" />
    <!-- bind 'addTodo' handler(ie listener) for component addTodo for '@add-todo' event -->
    <select v-model="filter">
      <option value="all">All</option>
      <option value="completed">Completed</option>
      <option value="in-progress">In progress</option>
    </select>
    <Loader v-if="loading" />
    <TodoList
      v-else-if="filteredTodos.length"
      v-bind:todos="filteredTodos"
      @remove-todo="removeTodo"
    />
    <p v-else>No todo items</p>
  </div>
</template>

<script>
import TodoList from "@/components/TodoList.vue";
import AddTodo from "@/components/AddTodo.vue";
import Loader from "@/components/Loader.vue";

export default {
  name: "app",
  data() {
    return {
      todosData: [],
      loading: true,
      filter: "all"
    };
  },
  components: {
    TodoList: TodoList,
    AddTodo: AddTodo,
    Loader //no need alias if the same name
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=3")
      .then(response => response.json())
      .then(json => {
        setTimeout(() => {
          console.log(
            "mounted() dom rendered Life cicle. fetch from api",
            json
          );
          this.todosData = json;
          this.loading = false;
        }, 1000);
      });
  },
  /*watch : {
      loading(value) {
          console.log('loading value', value);
      },
      filter(value) { // binded with v-model="filter"
          console.log('filter value', value);
      }
    }, Use @computed@ feature for filtering*/
  computed: {
    filteredTodos: function() {
      if (this.filter === "all") {
        return this.todosData;
      }
      if (this.filter === "completed") {
        return this.todosData.filter(t => t.completed);
      }
      if (this.filter === "in-progress") {
        return this.todosData.filter(t => !t.completed);
      }

      return this.todosData;
    }
  },
  methods: {
    removeTodo(id) {
      this.todosData = this.todosData.filter(t => t.id !== id);
    },
    addTodoHandler(todo) {
      console.log("Event @add-todo Handler fired. Param:", todo);
      this.todosData.push(todo);
    }
  }
};
</script>
