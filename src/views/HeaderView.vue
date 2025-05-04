<script setup lang="ts">
import NavItem from "../components/NavItem.vue";
</script>

<template>
  <header class="header">
    <div class="header__inner">
      <span class="header__title">My To-Do List</span>
      <nav class="header__nav">
        <ul class="header__nav-list">
          <NavItem to="/">Home</NavItem>
          <NavItem to="/about">About</NavItem>
        </ul>
      </nav>
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
    flex-wrap: wrap;
    padding: 1rem;
    width: 100%;
    max-width: 1920px;
    color: #fff;
  }

  &__title {
    font-size: 2rem;
    font-weight: 800;
    line-height: 2rem;
  }

  &__nav,
  &__nav-list {
    display: flex;
    align-items: center;
    justify-content: flex-end;
  }

  &__nav-list {
    list-style: none;
    gap: 1rem;
  }
}

@media screen and (max-width: 768px) {
  .header__title,
  .header__nav {
    width: 100%;
  }

  .header__nav,
  .header__nav-list {
    justify-content: flex-start;
  }
}
</style>
