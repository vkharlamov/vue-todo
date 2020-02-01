<template>
  <div>
    <h2>Todo Application</h2>
    <AddTodo @add-todo="addTodoHandler" />
    <!-- bind 'addTodo' handler(ie listener) for component addTodo for '@add-todo' event -->
    <hr />
    <TodoList v-bind:todos="todosData" @remove-todo="removeTodo" />
  </div>
</template>

<script>
import TodoList from "@/components/TodoList.vue";
import AddTodo from "@/components/AddTodo.vue";

export default {
  name: "app",
  data() {
    return {
      todosData: [
        /*{id: 1, title: "title#1", completed: false},
                    {id: 2, title: "title#2", completed: false},
                    {id: 3,  title: "title#3", completed: false}*/
      ]
    };
  },
  components: {
    TodoList: TodoList,
    AddTodo: AddTodo
  },
  mounted() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=3")
      .then(response => response.json())
      .then(json => {
        console.log("mounted() dom rendered Life cicle. fetch from api", json);
        this.todosData = json;
      });
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
