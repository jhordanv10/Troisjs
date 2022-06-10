<script lang="ts">
import { defineComponent, onMounted, ref } from 'vue';
import {
  Box,
  Camera,
  LambertMaterial,
  PointLight,
  Renderer,
  Scene,
  Sphere,
  AmbientLight,
  BasicMaterial,
  Texture,
  GltfModel,
} from 'troisjs';

export default defineComponent({
  name: 'Home',
  components: {
    Box,
    Camera,
    LambertMaterial,
    PointLight,
    Renderer,
    Scene,
    AmbientLight,
    Sphere,
    BasicMaterial,
    Texture,
    GltfModel,
  },
  setup() {
    const renderer = ref(null);
    const box = ref(null);
    const sphere = ref(null);

    function onReady() {
      console.log('Render is ready');
    }

    onMounted(() => {
      renderer?.value?.onBeforeRender(() => {
        box.value.mesh.rotation.x += 0.01;
        // sphere.value.mesh.rotation.y += 0.01;
      });
    });
    return {
      renderer,
      box,
      sphere,
      onReady,
    };
  },
});
</script>

<template>
  <div class="space">
    <Renderer resize="window" orbit-ctrl ref="renderer" alpha="0">
      <Camera :position="{ z: 10 }" />
      <Scene>
        <PointLight :position="{ y: 50, z: 50 }" />
        <AmbientLight />
        <Box ref="box" :rotation="{ y: Math.PI / 4, z: Math.PI / 4 }">
          <BasicMaterial color="#7F8487" />
        </Box>
        <Sphere
          ref="sphere"
          :position="{ x: 25, y: 10, z: -45 }"
          :radius="8"
          heightSegments="100"
        >
          <BasicMaterial color="#fff" />
        </Sphere>
        <GltfModel
          src="../../public/models/rocket/scene.gltf"
          @load="onReady"
          :position="{ x: -1, y: 0, z: 8 }"
          :rotation="{ x:Math.PI / -50}"
        />
      </Scene>
    </Renderer>
  </div>
</template>

<style>
.space {
  background-image: url('../../public/texture3.jpg');
  background-size: 100% 100vh;
  background-repeat: no-repeat;
}
</style>
