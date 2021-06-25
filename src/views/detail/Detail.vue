<template>
    <div id="detail">
      <detail-nav-bar class="detail-nav"></detail-nav-bar>
      <scroll class="content">
      <detail-swiper :top-images="topImages "></detail-swiper>
      <detail-base-info :goods="goods"></detail-base-info>
      <detail-shop-info :shop="shop"></detail-shop-info>
      </scroll>
      <detail-buttom-bar @addToCart="addToCart"></detail-buttom-bar>
    </div>
</template>

<script>
import DetailNavBar from "@/views/detail/childComps/DetailNavBar";
import {getDetail,Goods,Shop} from "@/network/detail";
import DetailSwiper from "@/views/detail/childComps/DetailSwiper";
import DetailBaseInfo from "@/views/detail/childComps/DetailBaseInfo";
import DetailShopInfo from "@/views/detail/childComps/DetailShopInfo";
import Scroll from "@/components/common/scroll/Scroll";
import DetailButtomBar from "@/views/detail/childComps/DetailButtomBar";

export default {
  name: "Detail",
  components: {DetailButtomBar, Scroll, DetailShopInfo, DetailBaseInfo, DetailSwiper, DetailNavBar},
  data(){
    return{
      iid:null,
      topImages:[],
      goods:{},
      shop:{}
    }
  },
  created() {
    console.log(this.$route.params.id);
    this.iid = this.$route.params.id
    getDetail(this.iid).then(res=>{
      console.log(res);
      const data = res.result;
      this.topImages = data.itemInfo.topImages
      // console.log(data.itemInfo.topImages);
      this.goods = new Goods(data.itemInfo, data.columns, data.shopInfo.services)
      // 3.创建店铺信息的对象
      this.shop = new Shop(data.shopInfo)
    })
  },
  methods:{
    addToCart() {
      // 1.创建对象
      const obj = {}
      // 2.对象信息
      obj.iid = this.iid;
      obj.imgURL = this.topImages[0]
      obj.title = this.goods.title
      obj.desc = this.goods.desc;
      obj.newPrice = this.goods.nowPrice;
      // 3.添加到Store中
      this.$store.commit('addCart', obj)
    },
  }
}
</script>

<style scoped>
#detail {
  position: relative;
  z-index: 9;
  background-color: #fff;
  height: 100vh;
}

.detail-nav {
  position: relative;
  z-index: 9;
  background-color: #fff;
}

.content {
  height: calc(100% - 44px);
}
</style>
