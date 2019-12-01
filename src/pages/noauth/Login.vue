<template>
  <q-layout>
    <q-page class="flex flex-center bg-primary">
      <div class="form-login shadow-4">
        <div class="logo-item">
          <img :src="logoPrivy">
        </div>
        <form class="form-input" @submit.prevent="inputLogin()">
          <div class="input-login">
            <q-input v-model="phone" placeholder="Phone Number" color="red-10" dense/>
          </div>
          <div class="input-login">
            <q-input v-model="password" type="password" placeholder="Password" color="red-10" dense/>
          </div>
          <div class="btn-container">
            <q-btn type="submit" label="LOGIN" color="primary" class="btn-item"/>
            <div class="text">Don't have access?</div>
            <router-link to="/register">
              <q-btn label="REGISTER" class="btn-item btn-register"/>
            </router-link>
          </div>
        </form>
      </div>
    </q-page>
  </q-layout>
</template>
<script>
import logoPrivy from '../../assets/icon/privyid_logo.png'
export default {
  data () {
    return {
      logoPrivy,
      phone: '',
      password: '',
      latitude: '-6.174023',
      longitude: '106.725207',
      latlong: '',
      // latitude: location.coords.latitude,
      // longitude: location.coords.longitude,
      location: null,
      gettingLocation: false,
      errorStr: null,
      device: '1', // for device type
      device_token: 'frfsgvrwe:APfdsafsgdfsgghfgfgjkhfsfgdhjhbvcvnetry767456fxsasdf'
    }
  },
  created () {
    // do we support geolocation
    if (!('geolocation' in navigator)) {
      this.$q.notify({ label: 'Geolocation is not available.', color: 'negative', position: 'top' })
      // this.errorStr = 'Geolocation is not available.'
      return
    }
    this.gettingLocation = true
    // get position
    navigator.geolocation.getCurrentPosition(pos => {
      this.gettingLocation = false
      this.location = pos
    }, err => {
      this.gettingLocation = false
      this.errorStr = err.message
    })
  },
  methods: {
    inputLogin () {
      this.$axios({
        method: 'post',
        url: 'http://pretest-qa.privydev.id/api/v1/oauth/sign_in',
        // url: 'anandabeniva/test',
        data: {
          phone: this.phone,
          password: this.password,
          latlong: (this.location.coords.latitude + ',' + this.location.coords.longitude),
          device_token: this.device_token,
          device_type: this.device
        }
      }).then(function (response) {
        console.log(response)
        console.log(response.status)
      }).catch(function (error) {
        console.log(error)
      })

      var self = this
      var postData = {
        data: {
          phone: this.phone,
          password: this.password,
          latlong: 'tes123',
          device_token: this.device_token,
          device_type: this.device
        }
      }
      self.axios.post('http://pretest-qa.privydev.id/api/v1/oauth/sign_in', {postData})
        .then(response => {
          console.log(response)
        })
        .catch(e => {
          console.log(e)
        })
    }
    // inputLogin () {
    //   var self = this
    //   var postData = {
    //     phone: self.phone,
    //     password: self.password,
    //     latlong: (self.location.coords.latitude + ',' + self.location.coords.longitude)
    //   }

    //   var formData = new FormData()
    //   for (var key in postData) {
    //     formData.append(key, postData[key])
    //   }
    //   this.$axios.post('http://pretest-qa.privydev.id/api/v1/oauth/sign_in', formData).then(function (response) {
    //     console.log(formData)
    //   }).catch(function (error) {
    //     console.log(error)
    //   })
    // }
  }
}
</script>
<style lang="stylus">
.input-login
  .q-input
    .q-field__inner
      .q-field__control
        .q-field__control-container
          .q-field__native
            text-align center
</style>
<style lang="stylus" scoped>
@import '~src/css/quasar.variables.styl'
.bg-primary
  background-color $color-privy !important
  .form-login
    @media only screen and (max-width: 1024px)
      width 70%
    @media only screen and (max-width: 480px)
      width 80%
    background-color #fff
    width 25%
    padding 15px 30px
    border-radius 8px
    text-align center
    // shadow
    // -webkit-box-shadow 0px 0px 13px -6px rgba(0,0,0,0.75)
    // -moz-box-shadow 0px 0px 13px -6px rgba(0,0,0,0.75)
    // box-shadow 0px 0px 13px -6px rgba(0,0,0,0.75)
    .logo-item
      text-align center
      img
        width 50%
    .form-input
      text-align center
      .input-login
        @media only screen and (max-width: 1024px)
          width 70%
        @media only screen and (max-width: 480px)
          width 100%
        width 90%
        margin auto
        padding 5px 0
      .btn-container
        text-align center
        padding 30px 0 20px 0
        .btn-item
          // @media only screen and (max-width: 1024px)
          //   width 80%
          width 80%
          border-radius 50px
        .btn-register
          background-color white
          border 1px solid $color-privy
          color $color-privy
        .text
          padding 15px
</style>
