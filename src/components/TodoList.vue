<template>
  <div class="header">
    <h1>My Todo List</h1>
    <img class="plus" src="/icons/plus-50.png" height="40" @click="addTodo" />
  </div>
  <TodoItem
    v-for="item in todos"
    :key="item.id"
    :todo="item"
    @delete-todo="handleDeleteTodo"
    @update-todo="updateTodo"
  />
</template>

<script setup lang="ts">
import TodoItem from "./TodoItem.vue";
import { ref, computed, onMounted } from "vue";

let todos = ref([
  { id: 2, title: "", isComplete: false },
  { id: 1, title: "", isComplete: false },
  { id: 0, title: "", isComplete: false },
]);

const handleDeleteTodo = (id: Number) => {
  todos.value = todos.value.filter((todo) => todo.id !== id);
};

const updateTodo = (payload: Object) => {
  const findtheSameId = (item) => item.id === payload.id;
  const index = todos.value.findIndex(findtheSameId);
  todos.value[index].title = payload.title;
  todos.value[index].isComplete = payload.isComplete;
  // console.log(todos.value);
};

const addTodo = () => {
  let item = {
    id: todos.value[0].id + 1,
    title: "",
    isComplete: false,
  };
  todos.value.unshift(item);
  // console.log(todos.value);
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
