<template>
  <div>
    <add-todo-item @addTodoItem="addTodoItem" />
    <ol>
      <todo-item
        v-for="item in items"
        :id="item.id"
        :text="item.text"
        :key="item.id"
        @editTodoItem="editTodoItem"
        @removeTodoItem="removeTodoItem"
      />
    </ol>
  </div>
</template>

<script>
import AddTodoItem from "./AddTodoItem.vue";
import TodoItem from "./TodoItem.vue";

export default {
  name: "TodoList",
  components: {
    AddTodoItem,
    TodoItem,
  },
  data() {
    let jsonItems = localStorage.getItem("todos");
    try {
      let items = JSON.parse(jsonItems);
      if (Array.isArray(items)) return { items };
      return { items: [] };
    } catch (e) {
      return { items: [] };
    }
  },
  watch: {
    items: {
      handler(newItems) {
        localStorage.setItem("todos", JSON.stringify(newItems));
      },
      deep: true,
    },
  },
  methods: {
    addTodoItem(text) {
      this.items.push({
        id:
          this.items
            .map((i) => i.id)
            .sort()
            .pop() + 1,
        text,
      });
    },
    editTodoItem(id, text) {
      let item = this.items.find((i) => i.id === id);
      item.text = text;
    },
    removeTodoItem(id) {
      let index = this.items.findIndex((i) => i.id === id);
      this.items.splice(index, 1); // or filter where !== index?
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>