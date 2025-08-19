<script setup lang="ts">
import NewsItem from './NewsItem.vue';

</script>

<template>
  <div class="news">
    <h2>Новости</h2>
    <NewsItem
      image="news1.jpg"
      title="Мечтаешь изменить мир и увидеть самые современные технологии?"
      discription="Тогда «Научная Вселенная» – для тебя! Победители отправятся на настоящий космодром!"
    />
    <NewsItem
      image="news2.jpg"
      title="Что стоит за этим знаком»: как нацпроекты меняют жизнь людей"
      discription="По нацпроекту «Молодежь и дети» продолжается работа по развитию образования"
    />
    <NewsItem
      image="news3.jpg"
      title="В этом году 84 жителя Марий Эл приняли участие во Всероссийском конкурсе Знание.Лектор"
      discription="Это уже пятый сезон конкурса, и он собрал рекордное количество участников — более 20 тысяч человек со всей страны"
    />
    <div class="more_news">
      <button class="more_news__btn">Показать ещё</button>
    </div>
  </div>
</template>

<style scoped lang="scss">
.news {
  width: 38rem;
  h2 {
    color: var(--title-color);
    font-family: "Ubuntu", sans-serif;
    font-weight: bolder;
  }

  @media (max-width: 1000px) {
    width: 100%;
  }
}

.more_news__btn {
  width: 100%;
  height: 3rem;
  background-color: var(--elements-bg-color);
  border: none;
  border-radius: 23px;
  color: #ffffff;
  font-weight: 700;
  cursor: pointer;
  transition: all 0.3s ease;
}

.more_news__btn:hover {
  transform: scale(1.03);
  background-color: var(--on-element-hover-color);
  transition: all 0.3s ease;
}
</style>