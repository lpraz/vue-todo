<template>
  <div>
    <input v-model="text" placeholder="Add new item..." />
    <button @click="addTodoItem">Add</button>
  </div>
</template>

<script>
export default {
  name: "AddTodoItem",
  emits: {
    addTodoItem: null,
  },
  data() {
    return {
      text: "",
    };
  },
  methods: {
    addTodoItem() {
      this.$emit("addTodoItem", this.text);
      this.text = "";
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>