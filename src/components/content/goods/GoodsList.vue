<template>
  <div class="goods">
<goods-list-item v-for="item in lists" :item="item"></goods-list-item>
  </div>
</template>

<script>
import GoodsListItem from "@/components/content/goods/GoodsListItem";
export default {
  name: "GoodsList",
  components: {GoodsListItem},
  props:{
    lists:{
      type:Array,
      default(){
        return []
      }
    }
  }
}

</script>

<style scoped>
.goods{
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  padding: 2px;
}
</style>
