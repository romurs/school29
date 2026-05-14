<script setup lang="ts">
useHead({
  title: 'Новость | 29',
})

const route = useRoute()
const newsId = route.params.id
const hasHistory = ref(false)

const router = useRouter()

onMounted(() => {
  hasHistory.value = window.history.length > 2
  loadNews()
})

const goBack = () => {
  if (hasHistory.value) {
    router.go(-1)
  } else {
    router.push('/allnews')
  }
}

interface News {
  id: number;
  title: string;
  content: string;
  created_at: string;
  updated_at: string;
  image?: string;
}

const config = useRuntimeConfig()
const apiUrl = config.public.apiUrl

const news = ref<News | null>(null)
const loading = ref(true)
const error = ref<string | null>(null)

// Загрузка данных в onMounted
const loadNews = async () => {
  try {
    loading.value = true
    error.value = null
    const response = await $fetch<News>(`${apiUrl}/news/${newsId}/`)
    news.value = response
  } catch (err) {
    console.error('Ошибка загрузки новости:', err)
    error.value = 'Не удалось загрузить новость'
  } finally {
    loading.value = false
  }
}

const formatDate = (dateString: string) => {
  const date = new Date(dateString)
  return date.toLocaleDateString('ru-RU', {
    day: 'numeric',
    month: 'long',
    year: 'numeric'
  })
}
</script>

<template>
  <div class="news-detail" v-if="!loading && news">
    <div class="news-header">
      <div class="news-detail__header">
        <button class="back-link" @click="goBack">← Назад</button>
        <h1>{{ news.title }}</h1>
        <div class="news-date">{{ formatDate(news.created_at) }}</div>
        <div class="news-updatedDate">Обновленно: {{ formatDate(news.updated_at) }}</div>
      </div>
      
      <div class="news-detail__image" v-if="news.image">
        <img :src="news.image" :alt="news.title" />
      </div>
    </div>
    
    <div class="news-detail__content">
      <p v-for="(paragraph, index) in news.content.split('\n')" :key="index">
        {{ paragraph }}
      </p>
    </div>
  </div>
  
  <div v-else-if="loading" class="loading">
    Загрузка...
  </div>
  
  <div v-else class="error">
    {{ error || 'Новость не найдена' }}
  </div>
</template>

<style scoped>
.news-detail {
  margin: 0 auto;
}

.news-header{
  background-color: var(--elements-bg-color);
  border-radius: 23px;
  padding: 20px;
}

.back-link {
  color: #000000;
  margin-bottom: 20px;
  display: inline-block;
  background-color: #e9e9e9;
  transition: all 0.3s ease;
  border-radius: 23px;
  padding: 10px;
  border: none;

  cursor: pointer;
}

.back-link:hover {
  transform: scale(1.03);
  transition: all 0.3s ease;
}

.news-detail__header h1 {
  /* font-size: 2rem; */
  margin: 10px 0;
}

.news-date {
  color: #000000;
  font-weight: 400;
  margin-bottom: 10px;
}

.news-updatedDate{
  color: var(--color-gray);
  font-weight: 300;
  font-style: italic;
  margin-bottom: 30px;
}

.news-detail__image img {
  width: 100%;
  height: auto;
  border-radius: 8px;
  margin-bottom: 30px;
}

.news-detail__content {
  line-height: 1.5;
  font-size: 1.1rem;
  font-weight: 400;
  padding: 20px;
}

.news-detail__content p {
  margin-bottom: 1.5rem;
  color: #000000;
}

.loading, .error {
  text-align: center;
  padding: 50px;
  font-size: 1.2rem;
}
</style>