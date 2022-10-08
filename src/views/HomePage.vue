<script setup>
import { onMounted } from 'vue'
import useAPI from '@/composables/useAPI'
import BaseTitle from '@/components/BaseTitle.vue'

const { categories, getCategories } = useAPI()

onMounted(async () => {
  await getCategories()
})
</script>

<template>
  <!--  -->
  <BaseTitle>
    <template #logo>
      <img src="/logo.svg" alt="logo" />
    </template>
    Triviantastic
  </BaseTitle>
  <div v-if="categories.length > 0" class="categories">
    <RouterLink v-for="category in categories" :key="category.id" :to="`/question/category/${category.id}`"
      class="category">
      {{ category.name }}
    </RouterLink>
  </div>
</template>

<style lang="postcss" scoped>
.categories {
  @apply grid flex-grow grid-cols-4 gap-12;

  & .category {
    @apply flex h-32 items-center justify-center rounded-lg border-4 border-green-500 py-4 text-center font-bold uppercase text-slate-600 transition-colors duration-300;

    &:hover {
      @apply cursor-pointer border-red-500 bg-red-500 text-white;
    }
  }
}
</style>
