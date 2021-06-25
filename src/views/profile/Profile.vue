<template>
<div class="profile">
  <profile-nav-bar></profile-nav-bar>
  <profile-user-info></profile-user-info>
  <profile-wallet></profile-wallet>
</div>
</template>

<script>
import ProfileNavBar from "@/views/profile/childComps/ProfileNavBar";
import ProfileUserInfo from "@/views/profile/childComps/ProfileUserInfo";
import ProfileWallet from "@/views/profile/childComps/ProfileWallet";
export default {
  name: "Profile",
  components: {ProfileWallet, ProfileUserInfo, ProfileNavBar}
}
</script>

<style scoped>

</style>
