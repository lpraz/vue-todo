<template>
  <div>
    <li v-show="!isEditing">
      <span>{{ text }} </span>
      <button @click="edit">Edit</button>
      <button @click="remove">Remove</button>
    </li>
    <li v-show="isEditing">
      <input v-model="editText" placeholder="Edit..." />
      <button @click="save">Save</button>
      <button @click="cancel">Cancel</button>
    </li>
  </div>
</template>

<script>
export default {
  name: "TodoItem",
  props: ["id", "text"],
  emits: {
    editTodoItem: null,
    removeTodoItem: null,
  },
  data() {
    return {
      editText: this.text,
      isEditing: false,
    };
  },
  methods: {
    edit() {
      this.isEditing = true;
    },
    save() {
      this.isEditing = false;
      this.$emit("editTodoItem", this.id, this.editText);
    },
    cancel() {
      this.isEditing = false;
      this.editText = this.text;
    },
    remove() {
      this.$emit("removeTodoItem", this.id);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>