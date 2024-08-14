<template>
  <Sidebar>
    <span class="colors-sidebar-title">Textures</span>
    <div class="colors-sidebar-grid">
      <SelectColor
          v-for="(color, index) in colors"
          :key="index"
          :active="color.image === currentTexture"
          v-bind="color"
          @click="selectColor(color.image)"
      />
    </div>
  </Sidebar>
</template>

<script setup>
import Sidebar from "@/components/Sidebar.vue";
import SelectColor from "@/components/SelectColor.vue";

const emit = defineEmits(['changeTexture']);

const colors = [
  {
    color: '#aabb3c',
    title: 'Flowers',
    image: 'textures/flowers.jpg'
  },
  {
    color: '#00bb33',
    title: 'Fibers',
    image: 'textures/fibers.jpg'
  },
];

const props = defineProps({
  currentTexture: {
    type: String,
    default: '',
  },
});

const selectColor = (color) => {
  emit('changeTexture', color);
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