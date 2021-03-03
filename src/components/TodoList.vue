<template>
  <div>
    <add-todo-item />
    <ol>
      <todo-item v-for="item in items" :text="item.text" :key="item.id" />
    </ol>
  </div>
</template>

<script>
import AddTodoItem from "./AddTodoItem.vue";
import TodoItem from "./TodoItem.vue";

export default {
  name: "TodoList",
  props: ["items"],
  components: {
    AddTodoItem,
    TodoItem,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>