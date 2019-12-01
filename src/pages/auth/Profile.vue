<template>
  <q-layout style="min-height: 550px">
    <section class="headline-page">
      <q-breadcrumbs active-color="red-10" color="light" align="right">
        <q-breadcrumbs-el class="q-body-2" label="Profile" to="/profile" />
        <!-- <q-breadcrumbs-el class="q-body-2" label="Insert" to="/admin/insert" /> -->
      </q-breadcrumbs>
    </section>
    <section class="content-page">
      <div class="box profile">
        <div class="box-title">
          <div class="row">
            <div class="text">Personal Profile</div>
            <div class="actions">
              <router-link to="/profile/update">
                <i class="fas fa-edit"></i>
              </router-link>
              <!-- <q-btn class="btn-edit" icon="fas fa-edit"></q-btn> -->
            </div>
          </div>
          <hr>
        </div>
        <div class="profile">
          <table>
            <tr>
              <td class="title">Name</td>
              <td>: </td>
              <td v-text="data.name"></td>
            </tr>
            <tr>
              <td class="title">Gender</td>
              <td>: </td>
              <td v-text="data.gender"></td>
            </tr>
            <tr>
              <td class="title">Birthday</td>
              <td>: </td>
              <td v-text="data.dob"></td>
            </tr>
            <tr>
              <td class="title">Hometown</td>
              <td>: </td>
              <td v-text="data.hometown"></td>
            </tr>
            <tr>
              <td class="title">Biodata</td>
              <td style="vertical-align: top;">: </td>
              <td class="biodata" v-text="data.biodata"></td>
            </tr>
          </table>
        </div>
      </div>
      <!-- education -->
      <div class="box education">
        <div class="box-title">
          <div class="row">
            <div class="text">Education</div>
            <div class="actions">
              <router-link to="/profile/update">
                <i class="fas fa-edit"></i>
              </router-link>
              <!-- <q-btn class="btn-edit" icon="fas fa-edit"></q-btn> -->
            </div>
          </div>
          <hr>
        </div>
        <div class="profile">
          <table>
            <tr>
              <td class="title">School Name</td>
              <td>: </td>
              <td v-text="data.school"></td>
            </tr>
            <tr>
              <td class="title">Graduated</td>
              <td>: </td>
              <td v-text="data.graduated"></td>
            </tr>
          </table>
        </div>
      </div>
      <!-- career -->
      <div class="box career">
        <div class="box-title">
          <div class="row">
            <div class="text">Career</div>
            <div class="actions">
              <router-link to="/profile/update">
                <i class="fas fa-edit"></i>
              </router-link>
              <!-- <q-btn class="btn-edit" icon="fas fa-edit"></q-btn> -->
            </div>
          </div>
          <hr>
        </div>
        <div class="profile">
          <table>
            <tr>
              <td class="title">Position</td>
              <td>: </td>
              <td v-text="data.position"></td>
            </tr>
            <tr>
              <td class="title">Company Name</td>
              <td>: </td>
              <td v-text="data.company"></td>
            </tr>
            <tr>
              <td class="title">Start Period</td>
              <td>: </td>
              <td v-text="data.start_period"></td>
            </tr>
            <tr>
              <td class="title">End Period</td>
              <td>: </td>
              <td v-text="data.end_period !== '' ? data.end_period : 'Now'"></td>
            </tr>
          </table>
        </div>
      </div>
    </section>
  </q-layout>
</template>
<script>
export default {
  data () {
    return {
      number: 1,
      data: {
        name: 'Fransiska Anindhita',
        gender: 'Female',
        dob: '04 February 1995',
        hometown: 'Kudus',
        biodata: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.',
        // school
        school: 'Dian Nuswantoro University',
        graduated: '2017',
        // career
        position: 'Front End Developer',
        company: 'Onero Solutions',
        start_period: '2017',
        end_period: ''
      }
    }
  },
  methods: {
    counter (value) {
      this.number = value + 1
    },
    getDataProfile () {
      var self = this
      this.$axios.get('http://pretest-qa.privydev.id/api/v1/profile/me').then(function (response) {
        self.data = response.data
        console.log(response.data)
      })
    }
  },
  created () {
    this.getDataProfile()
  }
}
</script>
<style lang="stylus" scoped>
.headline-page
  padding 30px
  // background-color #d3d3d3
  .q-headline
    font-size 16px
    color $color-privy
    font-weight 600
    letter-spacing 1px
.content-page
  padding 0 30px
  .box
    margin-bottom 25px
    padding 15px
    box-shadow 0px 2px 4px rgba(0, 0, 0, 0.16)
    .box-title
      position relative
      .text
        font-size 20px
        color $color-privy
      .actions
        i
          font-size 25px
          color $color-privy
          position absolute
          top 0
          right 0
          cursor pointer
          transition all ease .3s
          padding 5px
          border-radius 50px
          &:hover
            border-radius 4px
            background-color gray
            color white
        .btn-edit
          background-color $color-privy
          color white
          font-size 10px
          padding 10px
          border-radius 4px
      hr
        display block
        height 1px
        border 0
        border-top 2px solid #efefef
        margin 10px 0
        padding 0
    .profile
      font-size 16px
      table
        tr
          padding-bottom 10px
      .title
        color black
        font-size 16px
        font-weight 500
        vertical-align top
        min-width 140px
      .biodata
        max-width 500px
        text-align justify
</style>
