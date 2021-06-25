<template>
  <div class="category">
    <category-header></category-header>
    <category-lists></category-lists>
  </div>
</template>

<script>
import CategoryHeader from "@/views/category/childComps/CategoryHeader";
import CategoryLists from "@/views/category/childComps/CategoryLists";
export default {
  name: "Category",
  components: {CategoryLists, CategoryHeader}
}
</script>

<style scoped>

</style>
