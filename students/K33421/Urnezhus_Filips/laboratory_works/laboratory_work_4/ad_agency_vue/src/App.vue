<template>
 <v-app>
   <v-app-bar
     app
     color="primary"
     dark
   >
     <div class="d-flex align-center">
       <h1 class="headline">Рекламное агентство</h1>
     </div>

     <v-spacer></v-spacer>

     <v-btn v-if='auth' icon @click='AccountDetails'>
       <v-icon>mdi-account</v-icon>
     </v-btn>
     <div class="mx-2"></div>

     <v-btn icon @click='goHome'>
       <v-icon>mdi-home</v-icon>
     </v-btn>
     <div class="mx-2"></div>

     <v-btn icon>
       <v-icon v-if='!auth' @click='login' >mdi-login-variant</v-icon>
       <v-icon v-if='auth' @click='logout' >mdi-logout-variant</v-icon>
     </v-btn>

   </v-app-bar>

   <v-main class="d-flex align-center text-center">
     <router-view />
   </v-main>
 </v-app>
</template>

<script>
import $ from 'jquery'
export default {
  name: 'App',
  created () {
    if (localStorage.getItem('token')) {
      $.ajaxSetup({
        headers: {
          Authorization: 'Token ' + localStorage.getItem('token')
        }
      })
    }
  },

  computed: {
    auth () {
      if (localStorage.getItem('token')) {
        return true
      } else {
        return false
      }
    }
  },

  methods: {
    login () {
      this.$router.push({ name: 'signin' })
    },
    logout () {
      localStorage.removeItem('token')
      window.location = '/'
    },
    goHome () {
      this.$router.push({ name: 'about' })
    },
    AccountDetails () {
      this.$router.push({ name: 'accountdetails' })
    }
  },

  data: () => ({
    //
  })
}
</script>
