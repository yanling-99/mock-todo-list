<template>
  <div class="header">
    <h1>My Todo List</h1>
    <img class="plus" src="../../public/icons/plus-50.png" height="40" />
  </div>
  <TodoItem
    v-for="item in todos"
    :key="item.id"
    :todo="item"
    @delete-todo="handleDeleteTodo"
  />
</template>

<script setup lang="ts">
import TodoItem from "./TodoItem.vue";
import { ref } from "vue";

let todos = ref([
  {
    id: 0,
    title: "Get dressed",
    isComplete: false,
  },
  { id: 1, title: "Buy food", isComplete: false },
  { id: 2, title: "Eat lunch", isComplete: true },
  { id: 3, title: "Write Article", isComplete: true },
]);

const handleDeleteTodo = (id: Number) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};
</script>

<style scoped>
.header {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20px;
}
h1 {
  text-align: center;
  font-weight: bold;
}
h1,
.plus {
  margin-bottom: 2rem;
}
.plus {
  cursor: pointer;
}
</style>
