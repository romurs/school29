<script setup lang="ts">
import Links from '~/components/pages/index/Links.vue';


</script>

<template>
  <div class="main">
    <div class="main__container">
      <PagesIndexNews />
      <div class="contacts">
        <div class="contacts_container">
          <Links/>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.main {
  margin-top: 6.2rem;
  // min-height: 1550px;
  max-width: 1000px;
  margin-left: auto;
  margin-right: auto;
  font-weight: 400;

  
  border-bottom-left-radius: 23px;
  border-bottom-right-radius: 23px;
  background-color: var(--color-main-page);

  margin-bottom: 0.6rem;

  @media (max-width: 1000px) {
    margin-top: 3.2rem;
  }
}

.main__container {
  padding: 15px 25px;
  display: flex;
  flex-direction: row;

  @media (max-width: 1000px) {
    flex-direction: column;
    padding: 5px 10px;
  }
}

.contacts {
  height: 88rem;
  width: 20rem;
  border-radius: 23px;
  margin-left: auto;
  background-color: var(--elements-bg-color);

  @media (max-width: 1000px) {
    height: 75rem;
    width: 100%;
    margin-top: 10px;
  }
}

.contacts_container{
  margin: 10px;
  
}
</style>
