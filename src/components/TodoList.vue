<template>
  <div>
    <ul>
      <TodoItem
        v-for="(todoEl, i) of todos"
        v-bind:key="todoEl.id"
        v-bind:todo="todoEl"
        v-on:remove-todo="removeTodo"
        v-bind:idx="i"
      />
      <!--use "v-bind:key" to iterate. or getting error since 2.2.0-->
      <!--use "v-on:remove-todo" add event handler
                to bind the event describe act for click event for item
                v-on:click="$emit('remove-todo', todo.id)
            -->
    </ul>
  </div>
</template>
<script>
import TodoItem from "@/components/TodoItem";

export default {
  props: ["todos"],
  components: {
    TodoItem
  },
  methods: {
    removeTodo(id) {
      console.log("# ".id);
      this.$emit("remove-todo", id);
    }
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
}
</style>
