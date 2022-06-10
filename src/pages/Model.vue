<template>
  <div class="container">
    <Renderer ref="renderer" antialias orbir-ctrl resize="window">
        <Camera :position="{z: 50}"/>
        <Scene background="#E0DECA">
            <AmbientLight />
            <PointLight 
                color="#fff"
                :position="{x:100, y: 1000, z: 40 }"
                :intensity="20"
            />
            <GltfModel 
                src="../../public/models/ironman/scene.gltf"
                @load="onReady"
                :position="{x:0, y: -300, z: -1500}"
            />
        </Scene>
    </Renderer>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import {
  Camera,
  PointLight,
  Renderer,
  Scene,
  AmbientLight,
  GltfModel,
  
} from 'troisjs';

export default defineComponent({
  components: {
    Camera,
    PointLight,
    Renderer,
    Scene,
    AmbientLight,
    GltfModel,
  },
  setup() {
    function onReady() {
        console.log('Render is ready');
    }
    return {
        onReady
    }
  },
});
</script>

<style>

</style>