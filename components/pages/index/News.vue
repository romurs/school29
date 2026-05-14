<script setup lang="ts">
import NewsItem from "./NewsItem.vue";

// 1,77777778

const config = useRuntimeConfig();
const apiUrl = config.public.apiUrl;

interface News {
  id: number;
  title: string;
  content: string;
  created_at: string;
  image?: string;
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

const loadNews = async () => {
  try {
    loading.value = true;
    const data = await $fetch<ApiResponse>(`${apiUrl}/news/?page_size=3`)

      newsList.value = [...newsList.value, ...data.results];
      nextPage.value = data.next;
    
  } catch (err) {
    console.error("Ошибка:", err);
  } finally {
    loading.value = false;
  }
};

await loadNews();

const shortDiscription = (content: string) => {
  if (!content) return "";

  const sentenceEnd = content.match(/[.!?…]/);

  if (sentenceEnd) {
    return content.substring(0, sentenceEnd.index! + 1);
  }

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
      <NuxtLink to="/allnews">
        <button class="more_news__btn">Все новости</button>
      </NuxtLink>
    </div>
  </div>
</template>

<style scoped lang="scss">
.news {
  width: 38rem;
  h2 {
    color: #005f00;
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
