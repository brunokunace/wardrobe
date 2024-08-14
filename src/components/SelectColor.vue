<template>
  <div class="select-color" :class="{ active: active }">
    <div class="select-color-circle" :style="{ backgroundColor: color }">
      <img v-if="image" :src="image" class="select-color-image" :alt="image" />
    </div>
    <span class="select-color-name">
      {{ title }}
    </span>
  </div>
</template>

<script setup>
defineProps({
  color: {
    type: String,
    default: '',
  },
  title: {
    type: String,
    default: '',
  },
  image: {
    type: String,
    default: '',
  },
  active: {
    type: Boolean,
    default: false,
  },
});
</script>

<style lang="sass" scoped>
.select-color
  display: flex
  flex-direction: column
  align-items: center
  cursor: pointer
  width: 48px
  &:hover
    .select-color-circle
      opacity: 0.5
  &.active
    .select-color-circle
      box-shadow: #888 1px 2px 4px 1px
    .select-color-name
      font-weight: bolder
  &-circle
    width: 40px
    height: 40px
    outline: 2px solid #fff
    border-radius: 50%
    margin-bottom: 4px
  &-name
    font-family: Arial, sans-serif
    color: #555
    font-size: 10px
    user-select: none
    text-transform: uppercase
  &-image
    object-fit: cover
    width: 100%
    height: 100%
    border-radius: 50%
</style>