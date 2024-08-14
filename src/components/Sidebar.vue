<template>
  <div class="sidebar">
    <slot />
  </div>
</template>

<script setup>

</script>

<style lang="sass" scoped>
.sidebar
  display: flex
  flex-direction: column
  align-items: center
  border: 2px solid #c1c1c1
  border-radius: 8px
  padding: 16px
  background-color: #e1e1e1
  overflow: auto
</style>