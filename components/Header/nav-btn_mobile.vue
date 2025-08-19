<script setup lang="ts">
import Angle from "./Angle.vue";
defineProps({
  value: String,
  link: String,
});
</script>

<template>
  <div class="nav-btn">
    <div class="nav_angle">
      <Angle direction="right" />
    </div>
    <NuxtLink class="link" :to="link">{{ value }}</NuxtLink>
  </div>
</template>

<style scoped lang="scss">
.nav-btn {
  align-items: center;
  display: flex;
  padding: 10px;
  width: 100%;
  transition: all 0.3s ease;
}

.nav-btn:hover {
  a {
    color: #fff;
    scale: 1.05;
    transition: all 0.3s ease;
  }
}

.link {
  margin-left: 10px;
  color: #ffffff;
}

.nav_angle {
  height: 15px;
  width: 15px;
}
</style>
