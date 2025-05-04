<script setup lang="ts">
import HeaderView from "./views/HeaderView.vue";
import FooterView from "./views/FooterView.vue";
</script>

<template>
  <HeaderView />
  <div class="main-view__wrapper">
    <main class="main-view">
      <RouterView />
    </main>
  </div>
  <FooterView />
</template>

<style lang="scss" scoped>
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
</style>
