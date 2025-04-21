<script setup lang="ts">
//import NavItem from "../components/NavItem.vue";
</script>

<template>
  <header class="header">
    <div class="header__inner">
      <span class="site-title">My To-Do List</span>
    </div>
  </header>
</template>

<style lang="scss">
.header {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  background-color: #282928;

  &__inner {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem;
    width: 100%;
    max-width: 1920px;
    color: #fff;
  }

  .site-title {
    font-size: 2rem;
    font-weight: 800;
    line-height: 2rem;
  }
}
</style>
