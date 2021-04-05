<template>
  <li class="todo-item">
    <transition name="todo-view-edit">
      <span v-if="!isEditing">
        <span>{{ text }} </span>
        <button @click="edit">Edit</button>
        <button @click="remove">Remove</button>
      </span>
      <span v-else>
        <input v-model="editText" placeholder="Edit..." />
        <button @click="save">Save</button>
        <button @click="cancel">Cancel</button>
      </span>
    </transition>
  </li>
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
.todo-item {
  position: relative;
}

.todo-item > * {
  position: absolute;
}

.todo-view-edit-enter-active,
.todo-view-edit-leave-active {
  transition: opacity 0.3s linear;
}

.todo-view-edit-enter-from,
.todo-view-edit-leave-to {
  opacity: 0;
}
</style>