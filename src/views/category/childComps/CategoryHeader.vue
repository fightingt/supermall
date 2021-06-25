<template>
<div class="header">
  <nav-bar>
    <div slot="center" class="title">
      商品分类
    </div>
  </nav-bar>
</div>
</template>

<script>
import NavBar from "@/components/common/navbar/NavBar";
export default {
name: "CategoryHeader",
  components: {NavBar}
}
</script>

<style scoped>
.header{
  background-color:#ff5777;
}
.title{
  font-size: 18px;
  color: #f6f6f6;
}
</style>
