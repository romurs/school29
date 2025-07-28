<script setup lang="ts">

type Direction = 'up' | 'right' | 'down' | 'left';

const props = defineProps<{
  direction: Direction;
}>();

const rotationDegrees: Record<Direction, number> = {
  up: 0,
  right: 90,
  down: 180,
  left: 270
};

// Вычисляем стиль для transform
const imageStyle = computed(() => ({
  transform: `rotate(${rotationDegrees[props.direction]}deg)`
}));
</script>

<template>
  <img class="angle" src="../../public/angle-up.svg" :style="imageStyle"/>
</template>

<style scoped lang="scss">
.angle{
  width: 100%;
  height: 100%;
  display: block;
}
</style>