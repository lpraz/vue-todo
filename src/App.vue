<template>
  <todo-list :items="items" />
</template>

<script>
import TodoList from "./components/TodoList.vue";

export default {
  name: "App",
  data() {
    return {
      items: [
        {
          id: 1,
          text: "Finish this app"
        },
        {
          id: 2,
          text: "Learn more Haskell"
        }
      ]
    };
  },
  components: {
    TodoList,
  },
};
</script>

<style>
</style>