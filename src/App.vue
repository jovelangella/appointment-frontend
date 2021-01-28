<template>
  <v-app>
    <v-app-bar
      absolute
      app
      color="white"
      dense
      flat
      hide-on-scroll
    >
    <v-spacer />

      <v-btn icon href="https://www.instagram.com/stripmanila" target="_blank">

        <v-icon large color="purple darken-3">

         mdi-instagram

        </v-icon>

      </v-btn>

       <v-btn icon href="https://www.facebook.com/stripmanila/" target="_blank">

        <v-icon large color="purple darken-3">

         mdi-facebook

        </v-icon>

      </v-btn>

      <v-btn icon href="https://www.twitter.com/stripmanila/" target="_blnank">

        <v-icon large color="purple darken-3">

         mdi-twitter

        </v-icon>

      </v-btn>

      <!-- <div class="d-flex align-center"> -->
        <!-- <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        /> -->

        <!-- <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        /> -->
      <!-- </div> -->

      <!-- <v-spacer></v-spacer> -->

      <!-- <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn> -->
    </v-app-bar>

    <v-main>
      <v-row>

        <v-img
          alt="strip"
          contain
          class="mx-auto my-12"
          :src="images.company"
          height="300px"
          width="200px"
        />

      </v-row>

       <!-- <h1 class="purple--text text-md-center"
          >Hey Strip Mates!</h1>
       <h1 class="purple--text text-md-center"
       > Welcome to the Strip: Ministry of Waxing, the Global Authority in Hair Removal with 48 parlours in 12 major capital cities worldwide.</h1>

       <v-spacer /> -->

      <!-- <HelloWorld/> -->
      <!-- <Form/> -->
      <Test/>
    </v-main>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld'
// import Form from './components/Form'
import Test from './components/Test'

export default {
  name: 'App',

  components: {
    // HelloWorld,
    // Form
    Test
  },

  data: () => ({
    images: {
      company: require('@/assets/strip.jpg')
    }
  })
}
</script>
