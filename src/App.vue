<template>
  <v-app>
    <v-app-bar
      app
      dense
      flat
    >
    <v-spacer />

      <!-- facebook strip-->
      <template v-if="header">
        <v-btn icon href="https://www.facebook.com/stripmanila/" target="_blank">

          <v-icon large color="purple darken-3">

          mdi-facebook

          </v-icon>

        </v-btn>
      </template>

       <!-- facebook browhaus-->
      <template v-else>
        <v-btn icon href="https://www.facebook.com/BrowhausManila/" target="_blank">

          <v-icon large color="lime darken-3">

          mdi-facebook

          </v-icon>

        </v-btn>
      </template>

      <!-- twitter strip -->
      <template v-if="header">
        <v-btn icon href="https://twitter.com/stripmanila/" target="_blank">

          <v-icon large color="purple darken-3">

          mdi-twitter

          </v-icon>

        </v-btn>
      </template>

       <!-- twitter browhaus-->
      <template v-else>
        <v-btn icon href="https://twitter.com/browhausmanila" target="_blank">

          <v-icon large color="lime darken-3">

          mdi-twitter

          </v-icon>

        </v-btn>
      </template>

       <!-- instagram strip -->
      <template v-if="header">
        <v-btn icon href="https://www.instagram.com/stripmanila/" target="_blank">

          <v-icon large color="purple darken-3">

          mdi-instagram

          </v-icon>

        </v-btn>
      </template>

       <!-- instagram browhaus-->
      <template v-else>
        <v-btn icon href="https://www.instagram.com/browhausmanila/" target="_blank">

          <v-icon large color="lime darken-3">

          mdi-instagram

          </v-icon>

        </v-btn>
      </template>

    </v-app-bar>

    <v-main>

      <v-container>
      <v-row align="center" justify="center">
        <v-col align="center" justify="center">

          <template v-if="header">
            <v-img class="mb-n10"
              contain
              :src="images.strip"
              height="400px"
              width="300px"
            />
          </template>

          <template v-else>
            <v-img class="mb-n16"
              contain
              :src="images.browhaus"
              height="400px"
              width="300px"
            />
          </template>

        </v-col>

      </v-row>
      <v-row align="center" justify="center" class="mt-n16">
         <v-col align="center" justify="center">
           <template v-if="header">
              <h1 class="stripH1">Hey Strip Mates!</h1>
           </template>
           <template v-else>
              <h1 class="browhausH1">Hey Brow Buddy!</h1>
           </template>

         </v-col>
      </v-row>

       <v-row align="center" justify="center">
         <v-col md="6">
          <!-- <h1 class="text-justify.text-center stripH1"> Welcome to the Strip: Ministry of Waxing, the Global Authority in Hair Removal with 48 parlours in 12 major capital cities worldwide.</h1> -->
          <template v-if="header">
            <h1 class="text-justify.text-center stripH1"> Welcome to the Strip: Ministry of Waxing, the Global Authority in Hair Removal with 48 parlours in 12 major capital cities worldwide.</h1>
          </template>
          <template v-else>
            <h1 class="text-justify.text-center browhausH1"> Welcome to your one-stop brow and lash grooming salon built for you, the image-conscious urbanite who demands not just function, but function and style.</h1>
          </template>
         </v-col>
        </v-row>

       <v-spacer />

      <!-- <HelloWorld/> -->
      <!-- <Form/> -->
      <Test/>
      </v-container>
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
    header: false,
    images: {
      strip: require('@/assets/strip.jpg'),
      browhaus: require('@/assets/browhaus.png')
    }
  })
}
</script>

<style lang ="scss">
/* @import'@/assets/styles.scss'; */
@import url('http://fonts.cdnfonts.com/css/gotham');
@import url('https://www.cssfontstack.com/Helvetica');
.stripH1{
  font-family: 'Gotham Thin', sans-serif;
  text-align: center;
  color:#6A1B9A;
}
.browhausH1{
  font-family: Helvetica Neue,Helvetica,Arial,sans-serif;
  font-weight: 100;
  font-size: 35px;
  text-align: center;
  color:#9E9D24;
}

</style>
