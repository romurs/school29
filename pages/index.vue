<script setup lang="ts">
import Links from "~/components/pages/index/Links.vue";

useHead({
  title: "Главная | 29",
  meta: [{ name: "mainpage", content: "Главная страницы школы номер 29" }],
});
</script>

<template>
  <div class="main">
    <PagesIndexNews />
    <div class="contacts">
      <div class="contacts_container">
        <Links />
        <PagesIndexPhoneNumbers />
        <div class="school_map">
          <div style="position: relative; overflow: hidden">
            <a
              href="https://yandex.ru/maps/org/litsey_28/1338946939/?utm_medium=mapframe&utm_source=maps"
              style="color: #eee; font-size: 12px; position: absolute; top: 0px"
              >Лицей № 28</a
            ><a
              href="https://yandex.ru/maps/41/yoshkar-ola/category/lyceum/184106238/?utm_medium=mapframe&utm_source=maps"
              style="color: #eee; font-size: 12px; position: absolute; top: 14px"
              >Лицей в Йошкар‑Оле</a
            ><iframe
              src="https://yandex.ru/map-widget/v1/?ll=47.923966%2C56.633086&mode=poi&poi%5Bpoint%5D=47.923261%2C56.633138&poi%5Buri%5D=ymapsbm1%3A%2F%2Forg%3Foid%3D1338946939&z=16,5"
              width="100%"
              height="300"
              frameborder="1"
              allowfullscreen="true"
              style="position: relative"
            ></iframe>
          </div>
        </div>
          
        <div class="school_map-mobile">
          <div style="position: relative; overflow: hidden">
            <a
              href="https://yandex.ru/maps/org/litsey_28/1338946939/?utm_medium=mapframe&utm_source=maps"
              style="color: #eee; font-size: 12px; position: absolute; top: 0px"
              >Лицей № 28</a
            ><a
              href="https://yandex.ru/maps/41/yoshkar-ola/category/lyceum/184106238/?utm_medium=mapframe&utm_source=maps"
              style="color: #eee; font-size: 12px; position: absolute; top: 14px"
              >Лицей в Йошкар‑Оле</a
            ><iframe
              src="https://yandex.ru/map-widget/v1/?ll=47.923966%2C56.633086&mode=poi&poi%5Bpoint%5D=47.923261%2C56.633138&poi%5Buri%5D=ymapsbm1%3A%2F%2Forg%3Foid%3D1338946939&z=16,5"
              width="100%"
              height="400"
              frameborder="1"
              allowfullscreen="true"
              style="position: relative"
            ></iframe>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.main {
  display: flex;
  flex-direction: row;

  @media (max-width: 1000px) {
    flex-direction: column;
  }
}

.contacts {
  padding-bottom: 10px;
  width: 23rem;
  border-radius: 23px;
  margin-left: auto;
  background-color: var(--elements-bg-color);

  @media (max-width: 1000px) {
    padding-bottom: 10px;
    width: 100%;
    margin-top: 10px;
  }
}

@media (max-width: 1000px){
  .school_map{
    display: none;
  }
}

@media (min-width: 1000px){
  .school_map-mobile{
    display: none;
  }
}

.contacts_container {
  margin: 10px;
}
</style>
