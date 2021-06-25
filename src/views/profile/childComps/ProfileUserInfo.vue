<template>
<div class="user-info">
  <div class="img-info">
    <img src="~assets/img/profile/avatar.svg">
  </div>
  <div class="text-info">登陆/注册</div>
</div>
</template>

<script>
export default {
name: "ProfileUserInfo"
}
</script>

<style scoped>
.user-info{
  background-color: var(--color-tint);
  overflow: hidden;
}
.img-info img{
  float: left;
  margin-left: 30px;
  height: 100px;
  width: 100px;
}
.text-info{
  float: left;
  margin-top: 40px;
  margin-left: 20px;
  color: #fff;
  font-size: 20px;
}
</style>
