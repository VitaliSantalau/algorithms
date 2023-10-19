<script setup lang="ts">
  import LayoutHeader from './LayoutHeader.vue'
  import LayoutMain from './LayoutMain.vue'
  import LayoutFooter from './LayoutFooter.vue'
</script>

<template>
  <LayoutHeader />
  <LayoutMain>
    <slot></slot>
  </LayoutMain>
  <LayoutFooter />
</template>
