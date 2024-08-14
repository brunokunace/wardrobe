
<template>
  <div class="main">
    <ColorsSidebar
      class="main-sidebar-left"
      @change-color="changeColor"
      :current-color="currentColor"
    />
    <TexturesSidebar
      class="main-sidebar-right"
      @change-texture="changeTexture"
      :current-texture="currentTexture"
    />
    <ModelsSidebar
      class="main-sidebar-bottom"
      @change-model="changeModel"
      :current-model="currentModel"
    />
    <MainScene
      :color="currentColor"
      :texture="currentTexture"
      :model="currentModel"
    />
  </div>
</template>

<script setup>
import MainScene from "@/components/MainScene.vue";
import ColorsSidebar from "@/components/ColorsSidebar.vue";
import { ref } from "vue";
import TexturesSidebar from "@/components/TexturesSidebar.vue";
import ModelsSidebar from "@/components/ModelsSidebar.vue";

const currentColor = ref('');
const currentTexture = ref('');
const currentModel = ref('models/shirt.fbx');

const changeColor = (color) => {
  currentColor.value = color;
};

const changeTexture = (texture) => {
  currentTexture.value = texture;
};

const changeModel = (model) => {
  currentModel.value = model;
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
}
</style>

<style lang="sass" scoped>
.main
  display: flex
  position: relative
  &-sidebar
    &-left
      position: absolute
      top: 20px
      left: 20px
      bottom: 20px
    &-right
      position: absolute
      top: 20px
      right: 20px
      bottom: 20px
    &-bottom
      position: absolute
      left: 180px
      right: 180px
      bottom: 20px

</style>
