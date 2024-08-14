<template>
  <Sidebar>
    <span class="colors-sidebar-title">Colors</span>
    <div class="colors-sidebar-grid">
      <SelectColor
          v-for="(color, index) in colors"
          :key="index"
          :active="color.color === currentColor"
          v-bind="color"
          @click="selectColor(color.color)"
      />
    </div>
  </Sidebar>
</template>

<script setup>
import Sidebar from "@/components/Sidebar.vue";
import SelectColor from "@/components/SelectColor.vue";

const emit = defineEmits(['changeColor']);

const colors = [
  {
    color: '#aabb3c',
    title: '#aabb3c',
  },
  {
    color: '#00bb33',
    title: '#00bb33',
  },
  {
    color: '#1bc3ff',
    title: '#1bc3ff',
  },
  {
    color: '#f34823',
    title: '#f34823',
  },
  {
    color: '#ff2324',
    title: '#ff2324',
  },
];

const props = defineProps({
  currentColor: {
    type: String,
    default: '',
  },
});

const selectColor = (color) => {
  emit('changeColor', color);
};

</script>

<style lang="sass" scoped>
.colors-sidebar
  &-title
    color: #555
    font-family: Arial, sans-serif
    margin-bottom: 8px
  &-grid
    display: grid
    gap: 12px
    grid-template-columns: 1fr 1fr
</style>