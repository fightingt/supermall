<template>
<div class="profile-nav-bar">
  <nav-bar class="nav-bar">
    <div slot="center">我的档案</div>
  </nav-bar>
</div>
</template>

<script>
import NavBar from "@/components/common/navbar/NavBar";
export default {
  name: "ProfileNavBar",
  components: {NavBar}
}
</script>

<style scoped>
.nav-bar {
  background-color: var(--color-tint);
  font-weight: 700;
  color: #fff;
}
</style>
