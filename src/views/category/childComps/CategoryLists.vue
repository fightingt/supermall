<template>
  <div class="lists">
    <div v-for="(list,index) in lists"
         class="column"
         :class="{active:index===curIndex}"
         @click="listClick(index)">
      {{list}}
    </div>
  </div>
</template>

<script>
export default {
  name: "CategoryLists",
  data(){
    return {
      lists:['衣服','数码产品','日常用品','洗护','玩具','医疗','衣服','数码产品','日常用品','洗护','玩具','医疗','日常用品','洗护','玩具','医疗'],
      curIndex:0,
    }
  },
  methods:{
    listClick(index){
      this.curIndex = index
    }
  }
}
</script>

<style scoped>
.lists{
  display: flex;
  flex-direction: column;
  width: 80px;
  text-align: center;
}
.column{
  height: 45px;
  line-height: 45px;
  background-color: #f6f6f6;
  color: black;
}
.active{
  font-weight: 700;
  color: var(--color-high-text);
  background-color: #fff;
  border-left: 3px solid var(--color-high-text);
}

</style>
