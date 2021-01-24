<template>
  <div class="hello">
    <div class="input--container">
      <TodoInput @addThisTodo="addTodo" @handleTextChange="handleInput" />
    </div>
    <div class="list__item--wrapper">
      <TodoItem
        v-for="(todo, i) in todos"
        :key="i"
        :todo="todo"
        @toggleTodoItem="toggleTodo"
        @editTodoItem="editTodo"
        @removeTodoItem="removeTodo"
      />
    </div>
  </div>
</template>

<script>
import TodoItem from "./TodoItem";
import TodoInput from "./TodoInput";

export default {
  name: "TodoList",
  props: {
    msg: String,
  },
  components: {
    TodoItem,
    TodoInput,
  },
  data() {
    return {
      todoName: "",
      todos: [],
    };
  },
  methods: {
    handleInput(input) {
      this.todoName = input;
    },
    addTodo() {
      if (this.todoName.trim().length > 0) {
        const newTodo = {
          id: this.todos.length,
          name: this.todoName,
          isDone: false,
        };
        this.todos.push(newTodo);
        this.todoName = "";
      }
      return;
    },
    removeTodo(id) {
      this.todos = this.todos.filter((i) => i.id !== id);
    },
    toggleTodo(id) {
      this.todos[id].isDone = !this.todos[id].isDone;
    },
    editTodo(id) {
      if (this.todoName.trim().length > 0) {
        this.todos[id].name = this.todoName;
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="scss">
@mixin flexCenter($direction) {
  display: flex;
  flex-direction: $direction;
  justify-content: center;
  align-items: center;
}
input {
  border-radius: 0 !important;
}
.hello {
  @include flexCenter(column);
  max-width: 624px;
  font-weight: bold;
}
.input--container {
  display: flex;
}

.bg__done {
  background: rgb(182, 179, 179);
}
.bg__undone {
  background: rgb(47, 109, 73);
  color: white;
}
.item__done {
  width: 100%;
  text-decoration: line-through;
}
.item__undone {
  width: 100%;
}
.list__item--wrapper {
  width: 100%;
}
.list__item--container {
  @include flexCenter(row);
  padding-left: 10px;
}
.item {
  @include flexCenter(row);
  justify-content: flex-start;
  overflow-x: auto;
  margin-left: 10px;
  cursor: pointer;
}
.button__item {
  margin: 0 !important;
  border-radius: 0 !important;
}
</style>
