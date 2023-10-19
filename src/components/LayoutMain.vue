<template>
  <main>
    <div class="container">
      <slot></slot>
    </div>
  </main>
</template>

<style scoped>
  main {
    flex-grow: 1;
    background-color: var(--color-background);
  }
  .container {
    width: 100%;
    height: 100%;
    max-width: 1920px;
    margin: 0 auto;
    padding: 1rem;
  }
</style>
