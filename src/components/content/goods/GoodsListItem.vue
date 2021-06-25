<template>
<div class="good-list-item" @click="itemClick">
  <img :src="item.show.img" alt="">
  <div class="goods-info">
    <p>{{item.title}}</p>
    <span class="price">{{item.price}}</span>
    <span class="collect">{{item.cfav}}</span>
  </div>
</div>
</template>

<script>
export default {
  name: "GoodsListItem",
  props:{
    item:{
      type:Object,
      default(){
        return {}
      }
    }
  },
  methods:{
    itemClick() {
      this.$router.push("/detail/"+this.item.iid)
    }
  }
}
</script>

<style scoped>
.good-list-item{
  width: 45%;
  position: relative;
  padding-bottom: 40px;
}
.good-list-item img{
  width: 100%;
  border-radius: 5px;
}
.good-list-item .goods-info{
  position: absolute;
  bottom: 5px;
  left: 0px;
  right: 0px;
  text-align: center;
  font-size: 12px;
  /*overflow: hidden;*/
}
.goods-info p {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  margin-bottom: 3px;
}
.goods-info .price {
  color: var(--color-high-text);
  margin-right: 20px;
}
.goods-info .collect {
  position: relative;
}

.goods-info .collect::before {
  content: '';
  position: absolute;
  left: -15px;
  top: -1px;
  width: 14px;
  height: 14px;
  background: url("~assets/img/common/collect.svg") 0 0/14px 14px;
}
</style>
