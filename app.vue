<script setup lang="ts">
import FooterItem from "./components/FooterItem.vue";
import HeaderItem from "./components/HeaderItem.vue";
</script>

<template>
  <div class="wrapper">
    <HeaderItem />
    <main>
      <div class="container">
        <NuxtPage />
      </div>
    </main>
    <FooterItem />
  </div>
</template>

<style scoped lang="scss">
.wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
}

main {
  flex: 1 0 auto;
  margin-top: 6.2rem;

  @media (max-width: 1000px) {
    margin-top: 3.2rem;
  }
}

.container{
  
  max-width: 1000px;
  margin-left: auto;
  margin-right: auto;
  font-weight: 400;border-bottom-left-radius: 23px;
  border-bottom-right-radius: 23px;
  background-color: var(--color-main-page);
  margin-bottom: 0.6rem;

  
  padding: 15px 25px;
  @media (max-width: 1000px) {
    padding: 5px 10px;
  }
}
</style>
