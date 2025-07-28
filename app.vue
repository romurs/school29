<script setup lang="ts">
import FooterItem from "./components/FooterItem.vue";
import HeaderItem from "./components/HeaderItem.vue";
</script>

<template>
  <div class="wrapper">
    <HeaderItem />
    <main><NuxtPage /></main>
    <FooterItem />
  </div>
</template>


<style scoped lang="scss">
.wrapper{
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

main{
  flex: 1 0 auto;
}
</style>