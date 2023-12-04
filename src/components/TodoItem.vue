<template>
  <!-- todo.isComplete 待辦是否完成 -->
  <div :class="[todo.isComplete ? 'success' : 'error', 'todo-wrapper']">
    <!-- todo.title 待辦名稱 -->
    <textarea
      name="todoTitle"
      id="todoTitle"
      :cols="colNum"
      :rows="rowNum"
      :placeholder="placeHolder"
      class="todo-title"
      v-model="todoTitle"
      @keydown.enter.prevent
    ></textarea>
    <div class="todo-icons">
      <img :src="icons[0]" width="40" @click="switchIcon" />
      <img src="/icons/trash-48.png" width="40" @click="deleteItem" />
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";

const icons = ["/icons/check-50.png", "/icons/cancel-48.png"];
const switchIcon = () => {
  props.todo.isComplete = !props.todo.isComplete;
  let temp = icons[0];
  icons[0] = icons[1];
  icons[1] = temp;
};

const props = defineProps({
  todo: {
    type: Object,
    required: true,
  },
});
const todoTitle = ref(props.todo.title);
const placeHolder = "Please type here...";
const colNum = ref(30);
const rowNum = computed(() => {
  let defaultRows = Math.ceil(placeHolder.length / colNum.value);
  let realRows = Math.ceil(todoTitle.value.length / colNum.value);
  if (realRows > defaultRows) return realRows;
  else return defaultRows;
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
  align-items: center;
  gap: 10px;
  border-radius: 16px;
  box-shadow: 5px 0 5px rgba(0, 0, 0, 0.3);
  min-width: 400px;
  padding: 1rem 1.5rem;
  margin-top: 0.5rem;
}
.todo-title {
  font-size: 1.3rem;
  border: none;
  outline: none;
  overflow: hidden;
  resize: none;
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
