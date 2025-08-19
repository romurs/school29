<script setup lang="ts">
defineProps({
  image: {
    type: String,
    required: true
  },
  title: String,
  discription: String
});
</script>

<template>
  <div class="news__item">
    <div class="news_img" :style="{'--bg-image': `url(${image})`}">
      <img :src="image" alt="" />
    </div>
    <div class="news__informations">
      <div class="news_date">
        <div class="news_date__day">9</div>
        <div class="news_date__month-year">авг. 2025</div>
      </div>
      <div class="newes_text">
        <div class="title">
          <h3>{{ title }}</h3>
        </div>
        <div class="discription">
          <p>{{ discription }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.news__item {
  width: 100%;
  align-items: center;
  background-color: var(--elements-bg-color);
  border-radius: 23px;
  margin-bottom: 10px;
  transition: all 0.3s ease;
  cursor: pointer;
}

.news__item:hover{
  transform: scale(1.01);
  background-color: var(--on-element-hover-color);
  transition: all 0.3s ease;
}

.news_img {
  position: relative;
  height: 18rem;
  width: 100%;
  margin: 0 auto;
  overflow: hidden;

  border-radius: 23px;
  display: flex;
  justify-content: center;
  align-items: center;
}

.news_img::before {
  content: "";
  position: absolute;
  inset: 0;
  // background-image: url("/news1.jpg");
  background-image: var(--bg-image);
  background-position: center;
  background-size: cover;
  background-repeat: no-repeat;
  filter: blur(6px);
  z-index: 0;
}

.news_img img {
  max-height: 18rem;
  max-width: 100%;
  z-index: 1;
  position: relative;
}

.news__informations{
  display: flex;
}

.news_date{
  border-right: 1px solid var(--title-color);
  // border-right: 1px solid var(--color-yellow);
  margin: 10px;
  min-width: 4rem;
  text-align: right;
  padding-right: 10px;
}

.news_date__month-year{
  font-size: 0.9rem;
  color: var(--title-color);
}
.news_date__day{
  font-size: 1.4rem;
  color: var(--title-color);
  font-weight: 700;
}

.title {
  h3{
    font-weight: 700;
    color: var(--title-color);
  }
}
.discription {
  p{
    font-weight: 400;
    color: #fff;
  }
}
</style>
