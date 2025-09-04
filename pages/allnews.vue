<script setup lang="ts">
import NewsItem from '@/components/pages/index/NewsItem.vue';

useHead({
  title: 'Новости | 29',
  meta: [
    { name: 'allnews', content: 'Все новости школы номер 29' }
  ]
})

interface News {
  id: number;
  title: string;
  content: string;
  created_at: string;
  image?: string; // добавлено поле для изображения
}

interface ApiResponse {
  count: number;
  next: string | null;
  previous: string | null;
  results: News[];
}

const newsList = ref<News[]>([]);
const nextPage = ref<string | null>(null);
const loading = ref(false);

const loadNews = async (url?: string) => {
  try {
    loading.value = true;
    
    // Используем $fetch вместо useFetch для последующих запросов
    const data = await $fetch<ApiResponse>(url || 'http://localhost:8000/api/news/');

    newsList.value = [...newsList.value, ...data.results];
    nextPage.value = data.next;
    
  } catch (err) {
    console.error("Ошибка загрузки:", err);
  } finally {
    loading.value = false;
  }
};

await loadNews();

const loadMore = () => {
  if (nextPage.value) {
    loadNews(nextPage.value);
  }
};

const hasNextPage = computed(() => !!nextPage.value);

// Функция для форматирования даты
// const formatDate = (dateString: string) => {
//   const date = new Date(dateString)
//   const day = date.getDate()
//   const month = date.toLocaleString('ru', { month: 'short' })
//   const year = date.getFullYear()
//   return { day, month, year }
// }

const shortDiscription = (content: string) => {
  if (!content) return "";

  // Находим конец первого предложения
  const sentenceEnd = content.match(/[.!?…]/);

  if (sentenceEnd) {
    // Берем все до первого знака конца предложения + сам знак
    return content.substring(0, sentenceEnd.index! + 1);
  }

  // Если нет знаков препинания, берем первые 100 символов
  return content.length > 100 ? content.substring(0, 100) + "..." : content;
};
</script>

<template>
  <div class="news">
    <h2>Новости</h2>
    <NewsItem
      v-for="news in newsList"
      :key="news.id"
      :image="news.image || '/placeholder-news.jpg'"
      :title="news.title"
      :discription="shortDiscription(news.content)"
      :date="news.created_at"
      :id="news.id"
    />
    <div class="more_news">
      <button class="more_news__btn" v-if="hasNextPage" @click="loadMore" :disabled="loading">{{ loading ? 'Загрузка...' : 'Загрузить ещё' }}</button>
    </div>
  </div>
</template>

<style scoped lang="scss">

.news {
  width: 38rem;

  margin-left: auto;
  margin-right: auto;

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