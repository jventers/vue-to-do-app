<template>
  <div class="about-view">
    <h1>About</h1>
    <div clas="about-view__content">
      <p>
        This is a simple To-Do list application built in Vue 3 Composition API
        with TypeScript.
      </p>
      <p>
        It was based largely on the Google Keep application but was used as a
        sample/practice project for a coding bootcamp. It allows you to create,
        edit, and delete tasks.
      </p>
      <p>
        All of the code is open source, so feel free to explore making your own
        version.
      </p>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.about-view {
  display: flex;
  flex-direction: column;
  justify-content: flex-start;
  align-items: flex-start;
  gap: 1rem;
  width: 100%;
}
</style>
