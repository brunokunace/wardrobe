
<template>
  <div class="main">
    <ColorsSidebar
      class="main-sidebar-left"
      @change-color="changeColor"
      :current-color="currentColor"
    />
    <TexturesSidebar class="main-sidebar-right"
       @change-texture="changeTexture"
       :current-texture="currentTexture"
    />
    <MainScene
      :color="currentColor"
      :texture="currentTexture"
    />
  </div>
</template>

<script setup>
import MainScene from "@/components/MainScene.vue";
import ColorsSidebar from "@/components/ColorsSidebar.vue";
import { ref } from "vue";
import TexturesSidebar from "@/components/TexturesSidebar.vue";

const currentColor = ref('');
const currentTexture = ref('');

const changeColor = (color) => {
  currentColor.value = color;
}
const changeTexture = (texture) => {
  currentTexture.value = texture;
}
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

</style>
