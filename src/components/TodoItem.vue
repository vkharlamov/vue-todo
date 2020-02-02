<template>
  <li>
    <span v-bind:class="{ done: todo.completed }">
      <input type="checkbox" v-on:change="todo.completed = !todo.completed" />
      <strong>todo.id = {{ todo.id }}</strong>
      idx = {{ idx }}
      <b>{{todo.title | uppercase}}</b>
    </span>
    <button class="rm" v-on:click="$emit('remove-todo', todo.id)">
      &nbsp; remove
    </button>
  </li>
</template>

<script>
export default {
  props: {
    todo: {
      type: Object,
      required: true
    },
    idx: Number
  },
  filters: {
      uppercase(value) {
          return value.toUpperCase();
      }
  }
};
</script>
<style scoped>
li {
  border: 1px solid #ccc;
  display: flex;
  padding: 2px;
}
.done {
  text-decoration: line-through;
}
.rm {
}
</style>
