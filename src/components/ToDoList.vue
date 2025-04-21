<script setup lang="ts">
interface Props {
  title?: string;
}
const { title } = defineProps<Props>();
</script>

<template>
  <section
    class="todo-list"
    role="region"
    :aria-labelledby="title ? `section-${title}` : undefined"
  >
    <h2 v-if="title" class="todo-list__title" :id="`section-${title}`">
      {{ title }}
    </h2>
    <ul role="list" class="todo-list__items">
      <slot />
    </ul>
  </section>
</template>

<style scoped lang="scss">
.todo-list {
  display: flex;
  flex-direction: column;
  gap: 0.125rem;
  padding: 0 1rem;
  width: 100%;

  &__title {
    font-size: 1.5rem;
    font-weight: 600;
    margin-bottom: 0.5rem;
    color: #fff;
  }

  &__items {
    display: flex;
    flex-direction: column;
    gap: 0.5rem;
    width: 100%;
    list-style-type: none;
    padding: 0;
    margin: 0;
  }
}
</style>
