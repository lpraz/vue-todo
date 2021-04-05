<template>
  <div>
    <add-todo-item @addTodoItem="addTodoItem" />
    <transition-group name="todo-items" tag="ol">
      <todo-item
        v-for="item in items"
        :id="item.id"
        :text="item.text"
        :key="item.id"
        @editTodoItem="editTodoItem"
        @removeTodoItem="removeTodoItem"
        class="todo-item"
      />
    </transition-group>
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
    let items = this.parseJsonOrNull(jsonItems) || [];
    return { items };
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
      let lastId = this.items
        .map((i) => i.id)
        .sort()
        .pop();
      if (!lastId) lastId = 1;
      let id = lastId + 1;

      this.items.push({ id, text });
    },
    editTodoItem(id, text) {
      let item = this.items.find((i) => i.id === id);
      item.text = text;
    },
    removeTodoItem(id) {
      let index = this.items.findIndex((i) => i.id === id);
      this.items.splice(index, 1); // or filter where !== index?
    },
    parseJsonOrNull(json) {
      try {
        return JSON.parse(json);
      } catch (e) {
        return null;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.todo-items-enter-active {
  transition: all 0.3s ease-out;
}

.todo-items-leave-active {
  transition: all 0.3s ease-in;
}

.todo-items-enter-from {
  opacity: 0;
  transform: translateX(-30px);
}

.todo-items-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>