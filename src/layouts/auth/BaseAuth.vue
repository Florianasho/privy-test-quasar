<template>
  <!-- <div style="padding:30px;"> -->
  <div class="base-auth">
    <router-view />
  </div>
</template>

<style>
</style>

<script>
export default {
  beforeRouteEnter (to, from, next) {
    function checkLogin () {
      return localStorage.getItem(process.env.SESSION_PREFIX + 'id_token') !== null && localStorage.getItem(process.env.SESSION_PREFIX + 'access_token') !== null
    }
    if (!checkLogin()) {
      // next('/')
      next()
    } else {
      next()
    }
  }
}
</script>

<style lang="stylus" scoped>
</style>
