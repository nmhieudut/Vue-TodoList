<template>
  <div
    class="list__item--container"
    v-bind:class="todo.isDone ? 'bg__done' : 'bg__undone'"
  >
    <el-checkbox @click="toggleThisTodo" v-model="todo.isDone" />
    <div
      class="item"
      v-bind:class="todo.isDone ? 'item__done' : 'item__undone'"
    >
      {{ todo.name }}
    </div>
    <el-button
      @click="editThisTodo"
      class="button__item"
      type="warning"
      icon="el-icon-edit"
    />
    <el-button
      @click="removeThisTodo"
      class="button__item"
      type="danger"
      icon="el-icon-delete"
    />
  </div>
</template>
<script>
export default {
  name: "TodoItem",
  props: ["todo"],
  methods: {
    toggleThisTodo() {
      this.$emit("toggleTodoItem", this.todo.id);
    },
    editThisTodo() {
      this.$emit("editTodoItem", this.todo.id);
    },
    removeThisTodo() {
      console.log(this.todo.id);
      this.$emit("removeTodoItem", this.todo.id);
    },
  },
};
</script>
