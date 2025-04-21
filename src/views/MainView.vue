<script setup lang="ts">
import { ref, computed, nextTick } from "vue";
import ToDoList from "../components/ToDoList.vue";
import ToDoItem from "../components/ToDoItem.vue";

// Local state
interface ToDo {
  id: number;
  label: string;
  isCompleted: boolean;
}

// Create structure for To-Do item lists
const todos = ref<ToDo[]>([
  {
    id: Date.now(),
    label: "",
    isCompleted: false,
  },
]);

// Track the ID of the newly created item to auto-focus
const newlyCreatedId = ref<number | null>(null);

// Derived lists
const uncompleted = computed(() =>
  todos.value.filter((item) => !item.isCompleted)
);
const completed = computed(() =>
  todos.value.filter((item) => item.isCompleted)
);

function addToDoItem() {
  const newId = Date.now();
  todos.value.push({
    id: newId,
    label: "",
    isCompleted: false,
  });
  newlyCreatedId.value = newId;

  // Wait for DOM to update before resetting the flag
  nextTick(() => {
    newlyCreatedId.value = null;
  });
}

function deleteItem(id: number) {
  todos.value = todos.value.filter((todo) => todo.id !== id);
}

function toggleItem(id: number) {
  const index = todos.value.findIndex((todo) => todo.id === id);
  if (index === -1) return;
  const [item] = todos.value.splice(index, 1);
  item.isCompleted = !item.isCompleted;
  todos.value.push(item);
}
</script>

<template>
  <div class="main-view__wrapper">
    <main class="main-view">
      <!-- Uncompleted To-Dos -->
      <ToDoList title="To-Do">
        <ToDoItem
          v-for="todo in uncompleted"
          :key="todo.id"
          :autofocus="todo.id === newlyCreatedId"
          v-bind="todo"
          v-model:label="todo.label"
          @delete="deleteItem"
          @toggle="toggleItem"
        />
        <li class="add-btn__wrapper">
          <!-- Add Button -->
          <button class="add-btn" @click="addToDoItem">
            <span class="add-btn__icon">➕</span>Add To-Do Item
          </button>
        </li>
      </ToDoList>

      <!-- Completed To-Dos -->
      <ToDoList v-if="completed.length" title="Completed">
        <ToDoItem
          v-for="todo in completed"
          :key="todo.id"
          v-bind="todo"
          v-model:label="todo.label"
          @delete="deleteItem"
          @toggle="toggleItem"
        />
      </ToDoList>
    </main>
  </div>
</template>

<style lang="scss">
.main-view {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: center;
  gap: 2rem;
  width: 100%;
  max-width: 800px;
  color: #fff;
  padding: 2rem 0;

  &__wrapper {
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
    width: 100%;
    // height of viewport minus header and footer
    min-height: calc(100vh - 7rem);
  }
}
.add-btn {
  display: flex;
  justify-content: flex-start;
  align-items: center;
  padding: 0.5rem 0.75rem;
  font-size: 1rem;
  font-weight: 500;
  background: transparent;
  border-radius: 0.5rem;
  color: #fff;
  border: none;
  cursor: pointer;
  width: 100%;
  gap: 0.75rem;

  &__icon {
    font-family: "Segoe UI Symbol", "Noto Sans Symbols", sans-serif;
    color: inherit;
    font-size: inherit;
    line-height: 1rem;
  }

  &__text {
    color: inherit;
    font-size: inherit;
    line-height: 1rem;
  }

  &__wrapper {
    display: flex;
    width: 100%;
    height: 2.5rem;
  }

  &:hover {
    background: rgba(255, 255, 255, 0.1);
  }
}
</style>
