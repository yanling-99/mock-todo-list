<template>
  <!-- todo.isComplete 待辦是否完成 -->
  <div :class="[todo.isComplete ? 'success' : 'error', 'todo-wrapper']">
    <!-- todo.title 待辦名稱 -->
    <div class="todo-title">{{ todo.title }}</div>
    <div class="todo-icons">
      <img src="../../public/icons/check-50.png" width="40" />
      <img
        src="../../public/icons/trash-48.png"
        width="40"
        @click="deleteItem"
      />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from "vue";

const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
});

const emits = defineEmits(["delete-todo"]);
const deleteItem = () => {
  emits("delete-todo", props.todo.id);
};
</script>

<style scoped>
.todo-wrapper {
  display: flex;
  justify-content: space-between;
  border-radius: 16px;
  box-shadow: 5px 0 5px rgba(0, 0, 0, 0.3);
  min-width: 400px;
  padding: 1rem 1.5rem;
  margin-top: 0.5rem;
}
.todo-title {
  font-size: 1.5rem;
}

.todo-icons {
  display: flex;
  gap: 10px;
  cursor: pointer;
}
.success {
  border-left: 4px solid green;
}

.error {
  border-left: 4px solid red;
}
</style>
