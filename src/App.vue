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

      <v-btn icon href="https://www.twitter.com/stripmanila/" target="_blank">

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
      <v-row align="center" justify="center">
        <v-col align="center" justify="center">

          <v-img class="mx-16"
            alt="strip"
            contain
            :src="images.company"
            height="400px"
            width="300px"
          />

        </v-col>

      </v-row>
      <v-row align="center" justify="center" class="mt-n16">
         <v-col align="center" justify="center">
          <h1>Hey Strip Mates!</h1>
         </v-col>
      </v-row>

       <v-row align="center" justify="center">
         <v-col md="6">
          <h1 class="text-justify.text-center"> Welcome to the Strip: Ministry of Waxing, the Global Authority in Hair Removal with 48 parlours in 12 major capital cities worldwide.</h1>
         </v-col>
        </v-row>

       <v-spacer />

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

<style lang ="scss">
/* @import'@/assets/styles.scss'; */
@import url('http://fonts.cdnfonts.com/css/gotham');
h1{
  font-family: 'Gotham Thin', sans-serif;
  text-align: center;
  color:#4A148C;
}

</style>
