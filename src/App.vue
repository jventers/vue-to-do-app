<script setup lang="ts">
import HeaderView from "./views/HeaderView.vue";
import FooterView from "./views/FooterView.vue";
</script>

<template>
  <header-view />
  <router-view />
  <footer-view />
</template>
