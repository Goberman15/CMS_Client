<template>
  <div class="main">
    <CategoryList></CategoryList>
  </div>
</template>

<script>
import CategoryList from '@/components/CategoryList.vue'
export default {
  name: 'Category',
  components: {
    CategoryList
  }

}
</script>

<style scoped>
  .main {
    display: flex;
  }
</style>
