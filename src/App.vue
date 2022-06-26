<script setup lang="ts">
import { World, Model, ThirdPersonCamera, Dummy, Skybox, keyboard, types, LingoEditor } from 'lingo3d-vue';
import { ref } from 'vue';
const dummyRef = ref<types.Dummy>();

keyboard.onKeyPress = (_, pressed) => {
  const dummy = dummyRef.value;
  if (!dummy) return;
  if (pressed.has('w')) dummy.strideForward = -10;
  if (pressed.has('s')) dummy.strideForward = 10;
  if (pressed.has('a')) dummy.strideRight = 10;
  if (pressed.has('d')) dummy.strideRight = -10;
};
keyboard.onKeyDown = (key) => {
  const dummy = dummyRef.value;
  if (!dummy) return;
  if (key === 'Space') dummy.jump(15);
};
keyboard.onKeyUp = (_, pressed) => {
  const dummy = dummyRef.value;
  if (!dummy) return;
  if (!pressed.has('w') && !pressed.has('s')) dummy.strideForward = 0;
  if (!pressed.has('a') && !pressed.has('d')) dummy.strideRight = 0;
};
</script>

<template>
  <World>
    <Model
      pbr
      :x="162.62"
      :y="-82.06"
      :z="-351.3"
      physics="map"
      :width="221.88"
      :depth="252.94"
      :scale-x="400"
      :scale-y="400"
      :scale-z="400"
      src="Grassland.glb"
    />
    <ThirdPersonCamera
      :x="-240.05"
      :y="-638.23"
      :z="-1380.79"
      :rotation-x="-149.38"
      :rotation-y="3.14"
      :rotation-z="178.14"
      :inner-z="300"
      mouse-control
      active
    >
      <Dummy
        :animations="{
          idle: 'idle.fbx',
          running: 'running.fbx',
          runningBackwards: 'runningBackward.fbx',
          jumping: 'falling.fbx',
        }"
        toon
        pbr
        :x="-240.05"
        :y="-638.23"
        :z="-1380.79"
        physics="character"
        :width="20"
        :height="100"
        :depth="20"
        :scale-x="1.7"
        :scale-y="1.7"
        :scale-z="1.7"
        :rotation-y="-3.64"
        src="Fox.fbx"
        stride-move
        ref="dummyRef"
      />
    </ThirdPersonCamera>
    <Skybox texture="skybox.jpg"></Skybox>
    <Setup />
  </World>
</template>
