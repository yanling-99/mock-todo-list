<script setup lang="ts">
import TodoItem from "./TodoItem.vue";
import { ref } from "vue";

const todos = [
  {
    id: 0,
    title: "Get dressed",
    isComplete: false,
  },
  { id: 1, title: "Buy food", isComplete: false },
  { id: 2, title: "Eat lunch", isComplete: true },
  { id: 3, title: "Write Article", isComplete: true },
];
</script>

<template>
  <h1>My Todo List</h1>
  <TodoItem v-for="item in todos" :key="item.id" :todo="item" />
</template>

<style scoped>
h1 {
  text-align: center;
  margin-bottom: 2rem;
  font-weight: bold;
}
</style>
