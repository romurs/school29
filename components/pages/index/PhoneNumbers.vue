<script setup lang="ts">
import { NuxtLink } from '#components';

</script>

<template>
  <div class="phone_numbers">
    <!-- <h3>Номера телефонов</h3> -->
    <div class="directors_office">
      <h4>Приёмная директора:</h4>
      <p>+7 (8362) 21-56-88</p>
    </div>
    <div class="associate_director">
      <h4>Заместитель директора:</h4>
      <p>+7 (8362) 56-00-80</p>
    </div>
    <div class="watch">
      <h4>Вахта:</h4>
      <p> +7 (8362) 21-67-32</p>
    </div>
    <div class="schedule">
      <h4>Рабочие часы:</h4>
      <p>ПН-ПТ 08:00–19:00</p>
      <p>СБ 08:30–14:00</p>
    </div>
    <div class="location">
      <h4>Адрес:</h4>
      <NuxtLink to="https://yandex.ru/maps/-/CHxVJMNS">
        <p class="address">Марий-Эл, г.Йошкар-Ола, Ленинский проспект, д.10А</p>
      </NuxtLink>
    </div>
  </div>
</template>

<style scoped lang="scss">

.directors_office, .associate_director, .watch, .schedule, .location{
  p, h4{

  margin: 5px;
  }
  padding-top: 10px;

  .address{
    text-decoration-line: none;
  }

  .address:hover{
    text-decoration: underline;
  }
}
</style>