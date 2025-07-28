<script setup lang="ts">
import HeaderLogo from "./Header/HeaderLogo.vue";
import NavBtn from "./Header/nav-btn.vue";
import NavBtn_mobile from "./Header/nav-btn_mobile.vue";
import PageOverlay from "./Header/PageOverlay.vue";
import BurgerBtn from "./Header/BurgerBtn.vue";

const isScrolled = ref(false);
const isMenuOpen = ref(false);

const handleScroll = () => {
  isScrolled.value = window.scrollY > 20;
};

onMounted(() => {
  window.addEventListener("scroll", handleScroll);
});
onBeforeUnmount(() => {
  window.removeEventListener("scroll", handleScroll);
});

const toggleMenu = () => {
  isMenuOpen.value = !isMenuOpen.value;
};
</script>

<template>
  <PageOverlay :isMenuOpen="isMenuOpen" :toggle-fn="toggleMenu" />
  <header>
    <div class="header-container">
      <HeaderLogo :isScrolled="isScrolled" />
      <nav class="nav-btns" :class="{ 'nav-scrolled': isScrolled }">
        <NavBtn value="Сведения об организации" link="/information" />
        <NavBtn value="Приём в школу" link="/information" />
        <NavBtn value="Ученикам и родителям" link="/information" />
        <NavBtn value="Новости" link="/information" />
        <NavBtn value="Полоезная организация" link="/information" />
      </nav>
      <BurgerBtn :isMenuOpen="isMenuOpen" :toggleFn="toggleMenu" />
    </div>

    <transition name="menu-slide">
      <div class="mobile-menu" v-if="isMenuOpen" @click.stop>
        <NavBtn_mobile value="Сведения об организации" link="/vse" />
        <NavBtn_mobile value="Приём в школу" link="/negri" />
        <NavBtn_mobile value="Ученикам и родителям" link="/pidarasi" />
        <NavBtn_mobile value="Новости" link="/ebanyi" />
        <NavBtn_mobile value="Полезная организация" link="/rot" />
      </div>
    </transition>
  </header>
</template>

<style scoped lang="scss">
header {
  position: fixed;
  width: 100%;
  background-color: var(--color-green-bright);
  font-weight: 700;
  z-index: 1000;
}

.header-container {
  width: calc(100% - 100px);
  margin-left: auto;
  margin-right: auto;
  max-width: 1000px;
  display: flex;

  @media (max-width: 1000px) {
    margin-left: 0;
    margin-right: 0;
    width: 100%;
  }
}

.nav-btns {
  display: flex;
  flex: none;

  &.nav-scrolled {
    height: 3.2rem;
    transition: all 0.3s ease;
  }
  &:not(.nav-scrolled) {
    height: 6.2rem;
    transition: all 0.3s ease;
  }
  @media (max-width: 1000px) {
    display: none;
  }
}

.menu-slide-enter-active,
.menu-slide-leave-active {
  transition: all 0.3s ease;
  transform-origin: top;
}

.menu-slide-enter-from,
.menu-slide-leave-to {
  transform: translateY(-100%);
  opacity: 0;
}

.menu-slide-enter-to,
.menu-slide-leave-from {
  transform: translateY(0);
  opacity: 1;
}

.mobile-menu {
  position: absolute;
  top: 100%;
  left: 0;
  width: 100%;
  background-color: var(--color-main-page);
  z-index: 999;
}
</style>
