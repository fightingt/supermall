<template>
  <swiper>
    <slide v-for="item in banners">
      <a :href="item.link">
        <img :src="item.image" alt="">
      </a>
    </slide>
  </swiper>
</template>

<script>
import Swiper from "@/components/common/swiper/Swiper";
import Slide from "@/components/common/swiper/SwiperItem";
export default {
  name: "HomeSwiper",
  props:{
    banners:{
      type:Array,
      default(){
        return []
      }
    }
  },
  components:{
    Slide,
    Swiper
  }
}
</script>

<style scoped>

</style>
