<template>
  <Sidebar>
    <div class="models-sidebar-grid">
      <div
          v-for="(model, index) in models"
          :key="index"
          class="models-sidebar-model"
          @click="selectModel(model.model)"
      >
        <img :src="model.image" class="models-sidebar-image" :alt="model.image" />
      </div>
    </div>
  </Sidebar>
</template>

<script setup>
import Sidebar from "@/components/Sidebar.vue";

const emit = defineEmits(['changeModel']);

const models = [
  {
    model: 'models/dress.fbx',
    image: 'models/dress.png'
  },
  {
    model: 'models/shirt.fbx',
    image: 'models/shirt.png'
  },
];

const props = defineProps({
  currentModel: {
    type: String,
    default: '',
  },
});

const selectModel = (model) => {
  emit('changeModel', model);
};

</script>

<style lang="sass" scoped>
.models-sidebar
  &-grid
    display: flex
    gap: 12px
  &-model
    border: 1px solid #c1c1c1
    border-radius: 8px
    width: 80px
    height: 80px
    cursor: pointer
  &-image
    object-fit: cover
    width: 100%
    height: 100%
    border-radius: 8px
</style>