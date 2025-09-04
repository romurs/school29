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

const show = ref(false);
</script>

<template>
  <PageOverlay :isMenuOpen="isMenuOpen" :toggle-fn="toggleMenu" />
  <transition name="menu-slide">
    <div class="mobile-menu" v-if="isMenuOpen" @click.stop>
      <NavBtn_mobile
        value="Сведения об организации"
        link="/information"
        :toggleFn="toggleMenu"
      />
      <NavBtn_mobile
        value="Ученикам и родителям"
        link="/children_and_parents"
        :toggleFn="toggleMenu"
      />
      <NavBtn_mobile
        value="Приём в 1 класс"
        link="/receiving_to_1_class"
        :toggleFn="toggleMenu"
      />
      <NavBtn_mobile
        value="Приём в 10 класс"
        link="/receiving_to_10_class"
        :toggleFn="toggleMenu"
      />
      <NavBtn_mobile
        value="Заказать справку"
        link="/order_a_certificate"
        :toggleFn="toggleMenu"
      />
      <NavBtn_mobile
        value="Электронный дневник"
        link="https://sgo.mari-el.gov.ru/"
        :toggleFn="toggleMenu"
      />
    </div>
  </transition>
  <header>
    <div class="header-container">
      <HeaderLogo :isScrolled="isScrolled" />

      <!-- <transition name="popup_background">
        <div v-if="show" class="popup_background"></div>
      </transition> -->

      <nav
        class="nav-btns"
        :class="{ 'nav-scrolled': isScrolled }"
        @mouseenter="show = true"
        @mouseleave="show = false"
      >
        <NavBtn
          value="Сведения об организации"
          link="/information"
          :submenu="[
            { text: 'Документы', link: '/news' },
            { text: 'Руководство', link: '/team' },
            { text: 'Образовательные стандарты', link: '/download' },
          ]"
        />
        <!-- <NavBtn
          value="Ученикам и родителям"
          link="/students"
          :submenu="[
            { text: 'Приём в 1 класс', link: '/news' },
            { text: 'Приём в 10 класс', link: '/team' },
            { text: 'Электронный дневник', link: '/changelog' },
            { text: 'Заказать справку', link: '/download' },
          ]"
        /> -->
        <NavBtn value="Ученикам и родителям" link="/children_and_parents" />
        <NavBtn value="Приём в 1 класс" link="/receiving_to_1_class" />
        <NavBtn value="Приём в 10 класс" link="/receiving_to_10_class" />
        <NavBtn value="Заказать справку" link="/order_a_certificate" />
        <NavBtn
          value="Электронный дневник"
          link="https://sgo.mari-el.gov.ru/"
        />
        <!-- <NavBtn value="приём на работу" link="/information" /> -->
        <!-- <NavBtn value="Новости" link="/allnews" /> -->
        <!-- <NavBtn value="Полоезная организация" link="/information" /> -->
      </nav>
      <BurgerBtn :isMenuOpen="isMenuOpen" :toggleFn="toggleMenu" />
    </div>
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

.popup_background {
  background-color: #2e2e2eef;
  width: 100%;
  height: 200px;
  left: 0;

  position: absolute;
  top: 100%;
  border-bottom: 2px solid var(--color-red);
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
  top: 3.2rem;
  left: 0;
  width: 100%;
  background-color: #2e2e2eef;
  z-index: 999;
  padding-bottom: 20px;
  font-weight: 700;
}
</style>
