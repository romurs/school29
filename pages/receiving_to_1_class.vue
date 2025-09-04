<script setup lang="ts">
useHead({
  title: 'Приём в 1 класс | 29',
  meta: [
    { name: 'receiving to 1 class', content: 'Приём в 1 класс школы номер 29' }
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

const source = ref<DocumentItem[]>([]);

onMounted(async () => {
  try {
    const res = await fetch("http://localhost:8000/api/categories/5/");
    const data: CategoryResponse = await res.json();
    source.value = data.documents;
  } catch (err) {
    console.error("Ошибка загрузки:", err);
  }
});
</script>

<template>
  <div class="information">
    <h1>Приём в 1 класс</h1>
    <NuxtLink
      v-for="doc in source"
      :key="doc.id"
      :to="doc.file"
      target="_blank"
      class="doc"
    >
      <p class="inline text-blue-600 hover:underline">{{ doc.title }}</p></NuxtLink
    >
    <div class="more_documents-btn">
      <PagesIndexLinkBtn link="/alldocuments" logo="" value="Весь список документов"/>
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
.more_documents-btn{
  margin-top: 20px;
  width: 300px;
  justify-self: center;
}
</style>
