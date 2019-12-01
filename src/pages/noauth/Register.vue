<template>
  <q-layout>
    <q-page class="flex flex-center bg-primary">
      <div class="form-login shadow-4">
        <div class="logo-item">
          <img :src="logoPrivy">
        </div>
        <div class="title-register">REGISTER</div>
        <form class="form-input" @submit.prevent="submitData()">
          <div class="input-login">
            <q-input dense v-model="phone" label="Phone Number" placeholder="(ex: +6281XXXXXXXXX)" color="red-10" unmasked-value mask="+#############" :rules="[val => !!val || 'Field is required']"/>
          </div>
          <div class="input-login">
            <q-input dense v-model="password" type="password" label="Password" color="red-10" :rules="[val => !!val || 'Field is required']"/>
          </div>
          <div class="input-login">
            <q-select dense v-model="country" :options="optCountry" label="Country" color="red-10" :rules="[val => !!val || 'Field is required']"/>
          </div>
          <div class="input-login">
            <q-select dense v-model="device" :options="optDevice" label="Your Device Now" color="red-10" :rules="[val => !!val || 'Field is required']"/>
          </div>
          <div class="btn-container">
            <q-btn type="submit" label="REGISTER" color="primary" class="btn-item" @click="confirmRegister = true"/>
            <!-- <router-link to="register/phone">
              <q-btn label="REGISTER WITH PHONE" class="btn-item btn-login btn-phone"/>
            </router-link> -->
            <div class="text">Already have access?</div>
            <div class="link">
              <router-link to="/">
                <q-btn label="LOGIN" class="btn-item btn-login"/>
              </router-link>
            </div>
          </div>
        </form>
        <!-- <q-dialog class="dialog" v-model="confirmRegister">
          <q-card style="width: 300px">
            <q-card-section>
              <div class="text-h6">Small</div>
            </q-card-section>

            <q-card-section>
              Click/Tap on the backdrop.
            </q-card-section>

            <q-card-actions align="right" class="bg-white text-teal">
              <q-btn flat label="OK" v-close-popup />
            </q-card-actions>
          </q-card>
        </q-dialog> -->
      </div>
    </q-page>
  </q-layout>
</template>
<script>
import logoPrivy from '../../assets/icon/privyid_vertical.png'
export default {
  data () {
    return {
      logoPrivy,
      confirmRegister: false,
      phone: '',
      password: '',
      country: '',
      device: '', // for device type
      device_token: 'frfsgvrwe:APfdsafsgdfsgghfgfgjkhfsfgdhjhbvcvnetry767456fxsasdf',
      // latitude: '-6.174023',
      // longitude: '106.725207',
      latlong: '',
      location: null,
      gettingLocation: false,
      errorStr: null,
      otpCode: '',
      optCountry: [
        'Indonesia', 'Singapore', 'Malaysia'
      ],
      optDevice: [
        {
          value: '0',
          label: 'iOS'
        },
        {
          value: '1',
          label: 'Android'
        },
        {
          value: '2',
          label: 'Website'
        }
      ]
    }
  },
  created () {
    // do we support geolocation
    if (!('geolocation' in navigator)) {
      this.$q.notify({ label: 'Geolocation is not available.', color: 'negative', position: 'top' })
      this.errorStr = 'Geolocation is not available.'
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
  // submitData () {
    // var self = this
    // const headers = {
    //   'Content-Type': 'application/json',
    //   'X-Auth-Token': '97e0d315477f435489cf04904c9d0e6co',
    //   'Access-Control-Allow-Origin': '*'
    // }
    // var postData = {
    //   phone: self.phone,
    //   password: self.password,
    //   country: self.country,
    //   latlong: (self.location.coords.latitude + ',' + self.location.coords.longitude),
    //   device_token: self.device_token,
    //   device_type: self.device.value
    // }

    // var formData = new FormData()
    // for (var key in postData) {
    //   formData.append(key, postData[key])
    // }
    // this.$axios.post('http://pretest-qa.privydev.id/api/v1/register', formData, { headers }).then((response) => {
    //   console.log(response.headers)
    //   console.log(response.status)
    // }).catch(function (error) {
    //   console.log(error)
    // })
    // }
    submitData () {
      this.$axios({
        method: 'post',
        url: 'http://pretest-qa.privydev.id/api/v1/register',
        // url: 'anandabeniva/test',
        data: {
          phone: this.phone,
          password: this.password,
          country: this.country,
          latlong: (this.location.coords.latitude + ',' + this.location.coords.longitude),
          device_token: this.device_token,
          device_type: this.device.value
        }
      }).then(function (response) {
        console.log(response)
        console.log(response.status)
      }).catch(function (error) {
        console.log(error)
      })
    }
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
            text-align left
            // padding-left 5px
</style>
<style lang="stylus" scoped>
@import '~src/css/quasar.variables.styl'
.bg-primary
  background-color $color-privy !important
  .form-login
    @media only screen and (max-width: 1024px)
      width 70%
    @media only screen and (max-width: 480px)
      width 85%
    background-color #fff
    width 40%
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
        width 35%
    .title-register
      @media only screen and (max-width: 480px)
        font-size 18px
      padding 10px 0
      font-size 18px
      font-weight 700
      color darken($color-privy, 15%)
    .form-input
      text-align center
      .input-login
        @media only screen and (max-width: 1024px)
          width 80%
        @media only screen and (max-width: 480px)
          width 100%
        width 80%
        margin auto
        padding 0
        .q-input
          @media only screen and (max-width: 1024px)
            padding-bottom 10px
      .btn-container
        text-align center
        padding 30px 0 10px 0
        .btn-item
          @media only screen and (max-width: 1024px)
            width 80%
          @media only screen and (max-width: 480px)
            width 100%
          width 80%
          border-radius 50px
        .btn-login
          background-color white
          border 1px solid $color-privy
          color $color-privy
        .btn-phone
          margin 15px 0 0 0
        .text
          padding 30px 15px 0 15px
        .link
          padding 15px 0 0 0
          a
            text-decoration none
            color $color-privy
            .text-link
              font-weight 900
              font-size 14px
    .dialog
      background-color white
</style>
