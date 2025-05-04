<script setup lang="ts">
import { defineProps } from "vue";

interface NavItemProps {
  to: string;
}
const { to } = defineProps<NavItemProps>();
</script>

<template>
  <li class="nav-item">
    <RouterLink :to="to" class="nav-item__link">
      <slot />
    </RouterLink>
  </li>
</template>

<style lang="scss" scoped>
.nav-item {
  &__link {
    display: inline-block;
    padding: 0.5rem 1rem;
    color: #fff;
    text-decoration: none;
    border-radius: 0.5rem;
    transition: background-color 0.2s ease, color 0.2s ease;

    &:hover {
      background-color: rgba(255, 255, 255, 0.1); // subtle white hover
    }

    &.router-link-active {
      position: relative;

      &::after {
        content: "";
        position: absolute;
        bottom: -0.5rem;
        left: 0.25rem;
        width: calc(100% - 0.5rem);
        height: 0.25rem;
        background-color: #fff;
        border-radius: 0.125rem;
      }
    }
  }
}
</style>
