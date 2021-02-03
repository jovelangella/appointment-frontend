<template>

  <div>

    <v-container>

      <v-card
        class="mx-auto mt-5"
        max-width="500"
        :loading="loading"

      >
        <!-- App bar -->
        <v-app-bar
          elevation="4"
          color="#c5003e"
          dark
          height="100"

        >

          <v-app-bar-title class="appbartitle">Strip Appointment Time</v-app-bar-title>

            <v-spacer />

            <!-- Dark mode settings -->
            <v-btn
              icon
              @click="toggleTheme"
              flat
            >

            <v-icon v-if="this.$vuetify.theme.dark">mdi-brightness-4</v-icon>

            <v-icon v-else>mdi-brightness-5</v-icon>

            </v-btn>

          </v-app-bar>
          <!-- end of app bar -->

        <v-card-text>

          <v-container>

            <v-form
              ref="form"
              v-model="formHasErrors"
              lazy-validation
            >

              <!-- name -->
              <v-row>

                <v-col cols="12">

                  <v-text-field class="name"
                    v-model="form.clnt_nme"
                    :rules="rules.clnt_nme"
                    dense
                    outlined
                    label="Name"
                 />

                </v-col>

              </v-row>

              <!-- email -->
              <v-row class="mt-n5">

                <v-col class="6">

                  <v-text-field class="email"
                    v-model="form.emailadd"
                    :rules="rules.emailadd"
                    dense
                    outlined
                    label="Email"
                  />

                </v-col>

                <!-- number -->

                <v-col class="6">

                  <v-text-field
                    v-model="form.cel_numb"
                    :rules="rules.cel_numb"
                    maxlength="11"
                    counter
                    dense
                    outlined
                    label="Mobile Number"
                  />

                </v-col>

              </v-row>

              <!-- location-->
              <v-row class="mt-n5">

                <v-col class="12">

                  <v-select
                    v-model="form.locn_cde"
                    :items="locations"
                    item-text="locn_nme"
                    item-value="locn_cde"
                    :rules="[value => !!value||'Location is required']"
                    @change="retrieveLocationTime"
                    dense
                    outlined
                    label="Store Location"
                  >

                  </v-select>

                </v-col>

              </v-row>

              <!-- Appointment date -->
              <v-row class="mt-n5">

                <v-col class="6">

                  <v-menu
                    v-model="apnt_dte_Menu"
                    :close-on-content-click="false"
                    :nudge-right="40"
                    transition="scale-transition"
                    offset-y
                    min-width="auto"
                  >

                    <template v-slot:activator="{ on, attrs }">

                      <v-text-field
                        v-model="form.apnt_dte"
                        :rules="[value => !!value|| 'Appointment date is required']"
                        label="Date"
                        dense
                        readonly
                        outlined
                        v-bind="attrs"
                        v-on="on"
                      ></v-text-field>

                    </template>

                    <v-date-picker
                      v-model="form.apnt_dte"
                      :min="this.currentDay"
                      @input="apnt_dte_Menu = false, dayNumber, retrieveLocationTime()"
                    ></v-date-picker>

                  </v-menu>

                </v-col>

                <!-- time -->

                <v-col class="6">

                  <v-select
                    v-model="form.apnt_tme"
                    :items="locationTime"
                    item-text="std_time"
                    item-value="mil_time"
                    :rules="[value => !!value || 'Appointment time is required.']"
                    dense
                    outlined
                    label="Time"
                  />

                </v-col>

              </v-row>

              <!-- treatment -->
              <v-row class="mt-n5">

                <v-col cols="12">

                  <v-text-field
                    v-model="form.treatmnt"
                    dense
                    outlined
                    label="Treatment"
                  />

                </v-col>

              </v-row>

              <!-- message -->
              <v-row class="mt-n5">

                <v-col class="12">

                  <v-textarea
                    v-model="form.message_"
                    counter
                    outlined
                    dense
                    label="Message"
                    :rules="rules.message"
                  />

                </v-col>

              </v-row>

              <!-- buttons -->
              <v-card-actions class="mt-n5">

                  <v-spacer />

                  <!-- reset button -->
                  <v-btn @click="reset" small>

                    Reset

                  </v-btn>

                  <!-- submit button -->
                  <v-btn @click="submit" small :disabled="!formHasErrors">

                    Submit

                  </v-btn>

              </v-card-actions>

            </v-form>

          </v-container>

        </v-card-text>

      </v-card>

      <!-- snackbar -->
      <v-snackbar
        v-model="snackbar"
        :multi-line="multiLine"
      >

        {{ snackbarText  }}

        <template v-slot:action="{ attrs }">

          <v-btn
            color="red"
            text
            v-bind="attrs"
            @click="snackbar = false"
          >

            Close

          </v-btn>

        </template>

      </v-snackbar>

    </v-container>

  </div>

</template>

<script>
import axios from 'axios'
import moment from 'moment'

export default {
  data () {
    return {
      rules: {
        required: value => !!value || 'Required.',
        clnt_nme: [
          value => !!value || 'Name is required.',
          value => value.length <= 50 || 'Name must be less than 50 characters'
        ],
        cel_numb: [
          value => /^[0-9]+$/.test(value) || 'Input must be a number',
          value => !!value || 'Mobile number is required.',
          value => value.length === 11 || 'Mobile number must be 11 digits'
        ],
        emailadd: [
          value => !!value || 'E-mail is required',
          value => /.+@.+\..+/.test(value) || 'E-mail must be valid'
        ],
        message_: [value => value.length <= 25 || 'Max 25 characters']
      },
      locationTime: [],
      locations: [],
      formHasErrors: false,
      apnt_dte_Menu: false,
      btn_disabled: false,
      multiLine: true,
      snackbar: false,
      loading: false,
      errors: [],
      snackbarText: 'Thank you for making an appointment with us! We will contact you for confirmation shortly.',
      form: {
        clnt_nme: '',
        emailadd: '',
        cel_numb: '',
        locn_cde: '',
        apnt_dte: moment().add(1, 'days').format('YYYY-MM-DD'),
        apnt_tme: '',
        treatmnt: '',
        message_: ''
      }
    }
  },
  computed: {
    dayNumber () {
      var date = new Date(this.form.apnt_dte)
      return date.getDay()
    },
    currentDay () {
      return moment().add(1, 'days').format('YYYY-MM-DD')
    }
  },
  methods: {
    retrieveLocations () {
      axios.get('/locations', {
      })
        .then(response => {
          this.locations = response.data
        })
    },
    retrieveLocationTime () {
      axios.get('/time', {
        params: {
          locn_cde: this.form.locn_cde,
          day_numb: this.dayNumber
        }
      })
        .then(response => {
          this.locationTime = response.data
        })
    },
    submit () {
      this.$refs.form.validate() ? this.save() : this.$refs.form.validate()
    },
    save () {
      this.loading = true
      this.btn_disabled = true
      axios.post('/appointment/create', this.form)
        .then(response => {
          this.loading = false
          this.snackbar = true
          this.$refs.form.reset()
          response.status === 200 ? this.btn_disabled = false : this.btn_disabled = true
        })
        .catch(e => {
          const backendErrors = e.response.data.errors
          this.errors.push(backendErrors)
        })
    },
    reset () {
      this.$refs.form.reset()
    },
    toggleTheme () {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark
    }
  },

  created () {
    this.retrieveLocations()
  }
}

</script>
<style lang ="scss">
/* @import'@/assets/styles.scss'; */
@import url('http://fonts.cdnfonts.com/css/gotham');
.appbartitle {
  font-family: 'Gotham', sans-serif;
  text-align: center;
  color:white;
}

.v-text-field {
  font-family: 'Gotham', sans-serif;
}

</style>
