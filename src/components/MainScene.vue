<template>
  <div ref="target"></div>
</template>

<script setup>
import { onMounted, ref, watch } from 'vue';
import * as THREE from 'three';
import { OrbitControls } from 'three/addons/controls/OrbitControls.js';
import { FBXLoader } from 'three/examples/jsm/loaders/FBXLoader'

const target = ref();
const fbxLoader = new FBXLoader();
const textureLoader = new THREE.TextureLoader();
let scene;
let camera;
let renderer;
let model;

const props = defineProps({
  color: {
    type: String,
    default: '',
  },
  texture: {
    type: String,
    default: '',
  },
  model: {
    type: String,
    default: '',
  },
});

const animate = () => {
  renderer.render(scene, camera);
};
const onWindowResize = () => {
  const SCREEN_WIDTH = window.innerWidth;
  const SCREEN_HEIGHT = window.innerHeight;

  renderer.setSize( SCREEN_WIDTH, SCREEN_HEIGHT );

  camera.aspect = SCREEN_WIDTH / SCREEN_HEIGHT;
  camera.updateProjectionMatrix();
};
const createScene = () => {
  scene = new THREE.Scene();
  scene.background = new THREE.Color( 0xd2d2d2 );
  camera = new THREE.PerspectiveCamera(
      75,
      window.innerWidth / window.innerHeight,
      0.1,
      1000
  );
  camera.position.set(0.9, 0.8, 1.1)

  renderer = new THREE.WebGLRenderer({ alpha: true });
  renderer.setSize( window.innerWidth, window.innerHeight );

// scene.add(new THREE.AxesHelper(5))

  target.value.appendChild(renderer.domElement);
  renderer.setAnimationLoop( animate );
};
const createLights = () => {
  const ambientLight = new THREE.AmbientLight();
  const frontLight = new THREE.PointLight(0xffffff, 6);
  const backLight = frontLight.clone();

  frontLight.position.set(0.8, 1.4, 1.0);
  backLight.position.set(-0.8, 1.4, -1);

  scene.add(frontLight);
  scene.add(backLight);
  scene.add(ambientLight);
};
const createControls = () => {
  const controls = new OrbitControls(camera, renderer.domElement)
  controls.enableDamping = true
  controls.target.set(0, 0, 0)
};

const loadModel = (fileName) => {
  fbxLoader.load(fileName, (object) => {
    scene.remove(model);
    model = object;

    model.scale.set(.0015, .0015, .0015);
    model.position.y = - 1.6;
    scene.add(model);
  });
};

const changeColor = (color, meshName = '') => {
  if (!model) { return; }
  model.traverse((item) => {
    if (item.isMesh) {
      if (item.material instanceof Array) {
        item.material.map((material) => material.color.set(color));
        return;
      }
      item.material.color.set(color);
    }
  })
};

const changeTexture = (texturePath, meshName = '') => {
  if (!model) { return; }
  const texture = textureLoader.load(texturePath);
  texture.wrapS = THREE.MirroredRepeatWrapping;
  texture.wrapT = THREE.MirroredRepeatWrapping;
  texture.repeat.set(0.08, 0.08);

  model.traverse((item) => {
    if (item.isMesh) {
      const material = new THREE.MeshPhongMaterial({ map: texture });
      material.color.set(props.color);
      if (item.material instanceof Array) {
        item.material = item.material.map(() => material);
        return;
      }
      item.material = material;
    }
  });
};

watch(
    () => props.color,
    (value) => changeColor(value),
);

watch(
    () => props.texture,
    (value) => changeTexture(value),
);

watch(
    () => props.model,
    (value) => loadModel(value),
);

onMounted(() => {
  createScene();
  createLights();
  createControls();
  loadModel(props.model);
  window.addEventListener( 'resize', onWindowResize );
});
</script>


<style scoped>

</style>