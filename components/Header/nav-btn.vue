<script setup lang="ts">
defineProps({
  value: String,
  link: String,
  isScrolled: Boolean,
})
</script>

<template>
  <div class="nav-btn">
    <NuxtLink :to="link">{{ value }}</NuxtLink>
  </div>
</template>

<style scoped lang="scss">
.nav-btn{
  align-items: center;
  display: flex;
  padding: 10px;
  max-width: 100px;
  transition: all .3s ease;
}

.nav-btn:hover{
  a{
    color: #fff;
    scale: 1.05;
    transition: all .3s ease;
  }
}
</style>