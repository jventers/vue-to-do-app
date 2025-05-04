<script setup lang="ts">
import { ref, onMounted, nextTick } from "vue";

interface Props {
  id: number;
  isCompleted: boolean;
  autofocus?: boolean;
}

const { id, isCompleted = false, autofocus = false } = defineProps<Props>();

const label = defineModel<string>("label");
const inputRef = ref<HTMLInputElement | null>(null);

const emit = defineEmits<{
  (e: "delete", id: number): void;
  (e: "toggle", id: number): void;
}>();

function handleDelete() {
  emit("delete", id);
}

function handleToggle() {
  emit("toggle", id);
}

onMounted(() => {
  if (autofocus) {
    nextTick(() => {
      inputRef.value?.focus();
    });
  }
});
</script>

<template>
  <li class="todo-item" :class="{ 'todo-item--completed': isCompleted }">
    <div class="todo-item__check-and-label">
      <input
        class="todo-item__checkbox"
        type="checkbox"
        :checked="isCompleted"
        @change="handleToggle"
      />
      <input
        ref="inputRef"
        type="text"
        v-model="label"
        class="todo-item__label"
      />
    </div>
    <button
      class="todo-item__delete-btn"
      @click="handleDelete"
      aria-label="Delete Item"
    >
      ✕
    </button>
  </li>
</template>

<style scoped lang="scss">
.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 0.75rem;
  padding: 0.25rem 0.75rem;
  width: 100%;
  border: 1px solid transparent;

  &__check-and-label {
    width: 100%;
    display: flex;
    align-items: center;
    gap: 0.75rem;
    justify-content: flex-start;
  }

  &__checkbox {
    color: #fff;
    cursor: pointer;
    width: 0.9rem;
    height: 0.9rem;
    margin: 0.1rem;
  }

  &__label {
    flex: 1;
    height: 2rem;
    font-size: 1rem;
    padding-top: 1px;
    border: none;
    background: transparent;
    color: inherit;
    color: #fff;

    &:focus {
      outline: none;
    }
  }

  &__delete-btn {
    all: unset;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 2rem;
    max-width: 2rem;
    height: 2rem;
    max-height: 2rem;
    background: none;
    border: none;
    border-radius: 0.5rem;
    font-size: 1.25rem;
    color: #ccc;
    cursor: pointer;
    aspect-ratio: 1 / 1;
    opacity: 0;
    pointer-events: none;

    &:hover {
      color: #fff;
      background-color: rgba(255, 255, 255, 0.1);
    }
  }

  &--completed {
    opacity: 0.6;

    .todo-item__label {
      text-decoration: line-through;
    }
  }

  &:hover .todo-item__delete-btn,
  &:focus-within .todo-item__delete-btn {
    opacity: 1;
    pointer-events: auto;
  }

  &:hover,
  &:focus-within {
    border-top: 1px solid rgba(255, 255, 255, 0.1);
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }
}
</style>
