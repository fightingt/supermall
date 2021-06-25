<template>
  <swiper>
    <slide v-for="item in banners">
      <a :href="item.link">
        <img :src="item.image" alt="" @load="imageLoad">
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
  },
  methods:{
    imageLoad(){
      // console.log("------")
      this.$emit("swiperImageLoad")
    }
  }
}
</script>

<style scoped>

</style>
