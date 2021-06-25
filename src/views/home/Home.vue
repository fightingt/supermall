<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <tab-control :titles="['流行', '新款', '精选']"
                 @tabClick="tabClick"
                 ref="tabControl1"
                 class="tab-control2" v-show="isFixed"/>
    <scroll class="content"
            ref="scroll"
            :probetype="3"
            @scroll="showBacktop"
            :pull-up-load="true"
            @pullingUp="loadMore">
    <home-swiper :banners="banners" @swiperImageLoad="swiperImageLoad"></home-swiper>
    <recommend-view :recommends="recommends"></recommend-view>
    <feature-view></feature-view>
    <tab-control :titles="['流行', '新款', '精选']" class="tab-control"
                 @tabClick="tabClick"
                 ref="tabControl"></tab-control>
    <goods-list :lists="showGoods"></goods-list>
    </scroll>
    <back-top @click.native="backClick" v-show="isShowTop"></back-top>
  </div>
</template>

<script>
import NavBar from "@/components/common/navbar/NavBar";
import HomeSwiper from "@/views/home/childComps/HomeSwiper";
import {getHomeMultidata, getHomeGoods} from "@/network/home"
import RecommendView from "@/views/home/childComps/RecommendView";
import FeatureView from "@/views/home/childComps/FeatureView";
import TabControl from "@/components/content/tabControl/TabControl";
import GoodsList from "@/components/content/goods/GoodsList";
import Scroll from "@/components/common/scroll/Scroll";
import BackTop from "@/components/content/backTop/BackTop";

export default {
  name: "Home",
  components: {BackTop, Scroll, GoodsList, TabControl, FeatureView, RecommendView, HomeSwiper, NavBar},
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        'pop': {page: 0, list: []},
        'new': {page: 0, list: []},
        'sell': {page: 0, list: []}
      },
      currentType: 'pop',
      isShowTop: false,
      tabOffsetTop:0,
      isFixed:false
    }
  },
  created() {
    this.getHomeMultidata()

    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')
  },
  computed:{
    showGoods(){
      return this.goods[this.currentType].list
    },
  },
  methods: {

    /**
     * tabbar 相关方法
     */
    backClick(){
      this.$refs.scroll.scrollTo(0,0)
    },

    tabClick(index) {
      switch (index) {
        case 0:
          this.currentType = 'pop';
          break;
        case 1:
          this.currentType = 'new';
          break
        case 2:
          this.currentType = 'sell';
          break;
      }
      this.$refs.tabControl1.currentIndex = index;
      this.$refs.tabControl.currentIndex = index;
    },
    showBacktop(position){
      this.isShowTop = (-position.y)>1000

      this.isFixed = (-position.y)>this.tabOffsetTop
    },
    loadMore(){
      this.getHomeGoods(this.currentType)
    },
    swiperImageLoad(){
      this.tabOffsetTop = this.$refs.tabControl.$el.offsetTop
    },
    /**
     * 网络请求相关方法
     */
    getHomeMultidata() {
      getHomeMultidata().then(res => {
        //console.log(res)
        this.banners = res.data.banner.list
        this.recommends = res.data.recommend.list
      })
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1
      getHomeGoods(type, page).then(res => {
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page += 1
        this.$refs.scroll.finishPullUp()
      })

    }
  }
}
</script>

<style scoped>
#home {
  /*margin-top: 44px;*/
  height: 100vh;
  position: relative;
}

.home-nav {
  background-color: var(--color-tint);
  color: #fff;

  /*position: fixed;*/
  /*left: 0;*/
  /*right: 0;*/
  /*top: 0;*/
  /*z-index: 9;*/
}

/*.tab-control {*/
/*  position: sticky;*/
/*  top: 44px;*/
/*  z-index: 9;*/
/*}*/
.content{
  overflow: hidden;
  position: absolute;
  top: 44px;
  bottom: 49px;
  left: 0;
  right: 0;
}
.tab-control2 {
  position: relative;
  z-index: 9;
}
</style>
