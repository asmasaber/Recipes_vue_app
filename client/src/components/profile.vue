<template>
  <v-layout row wrap>
    <v-flex xs12>
      <v-stepper vertical>
        <v-layout row wrap>
          <v-flex xs2>
            <v-stepper-step editable step="1">Profile Info</v-stepper-step>
            <v-stepper-step editable step="2">Change Password</v-stepper-step>
            <v-stepper-step editable step="3">Your Recipes</v-stepper-step>
          </v-flex>
          <v-flex xs10>
            <v-stepper-content step="1">
              <Profile></Profile>
            </v-stepper-content>
             <v-stepper-content step="2">
              <div class="mb-5" height="200px">
                <ChangePassword></ChangePassword>
              </div>
            </v-stepper-content>
            <v-stepper-content step="3">
              <div class="mb-5" height="200px">
                <Recipes></Recipes>
              </div>
            </v-stepper-content>
          </v-flex>
        </v-layout>
      </v-stepper>
    </v-flex>
  </v-layout>
</template>

<script>
import Recipes from './user-Recipes.vue'
import Profile from './edit-profile.vue'
import ChangePassword from './change-password.vue'
import AuthService from '@/services/AuthService'

import { mapState } from 'vuex'

export default {
  data () {
    return {
      e13: 2
    }
  },
  computed: {
    ...mapState([
      'isUserLoggedIn',
      'user'
    ])
  },
  async created () {
    // if (!this.isUserLoggedIn) {
    //   this.$router.push({ name: 'login' })
    // }
  },
  route: {
    // Check the users auth status before
    // allowing navigation to the route
    canActivate () {
      console.log('can activate')
      return AuthService.user.authenticated
    }
  },
  components: {
    Recipes,
    Profile,
    ChangePassword
  }
}
</script>

<style>
.theme--light.v-stepper--vertical .v-stepper__content:not(:last-child) {
    border-left: 0;
}

</style>
