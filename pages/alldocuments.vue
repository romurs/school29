<script setup lang="ts">
import { ref, onMounted } from "vue";

useHead({
  title: 'Документы | 29',
  meta: [
    { name: 'mainpage', content: 'Главная страницы школы номер 29' }
  ]
})

interface DocumentItem {
  id: number;
  title: string;
  file: string;
}

interface CategoryResponse {
  id: number;
  name: string;
  documents: DocumentItem[];
}

const allDoc = ref<CategoryResponse[]>([]);

onMounted(async () => {
  try {
    const res = await fetch("http://localhost:8000/api/categories/");
    const data: CategoryResponse[] = await res.json();
    allDoc.value = data.filter(cat => cat.documents && cat.documents.length > 0);
  } catch (err) {
    console.error("Ошибка загрузки:", err);
  }
});
</script>

<template>
  <div>
    <div
      v-for="category in allDoc"
      :key="category.id"
      class="information"
    >
      <h1>{{ category.name }}</h1>

      <NuxtLink
        v-for="doc in category.documents"
        :key="doc.id"
        :to="doc.file"
        target="_blank"
        class="doc"
      >
        <p class="inline text-blue-600 hover:underline">{{ doc.title }}</p>
      </NuxtLink>
    </div>
  </div>
</template>


<style scoped lang="scss">
.information{
  h1, p{
    color: black;
  }

  p{
    display: inline;
  }

  .doc{
    display: inline-block; // меняем на inline-block
    margin-left: 20px;

    font-weight: 400;
    font-style: italic;
    margin-top: 10px;
  }

  p:hover{
    text-decoration: underline;
  }
}
</style>
