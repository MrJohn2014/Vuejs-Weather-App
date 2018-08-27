<template >
  <v-footer
    dark
    height="auto"
  >
    <v-card
      flat
      tile
      class="indigo lighten-1 white--text text-xs-center footer_layout"

    >
      <v-card-text>
        <v-btn
          v-for="icon in icons"
          :key="icon"
          class="mx-3 white--text"
          icon
        >
          <v-icon size="24px">{{ icon }}</v-icon>
        </v-btn>
      </v-card-text>
         Weather Data are from OpenWeatherMap API
      <v-card-text class="white--text pt-0">

      </v-card-text>

      <v-divider></v-divider>

      <v-card-text class="white--text">
        &copy;2018 — <strong>Vuetify</strong>
      </v-card-text>
    </v-card>
  </v-footer>
</template>



<script>
export default {
    name: 'Footer',
    data:()=>({
     icons:[
      'fab fa-facebook',
      'fab fa-twitter',
      'fab fa-google-plus',
      'fab fa-linkedin',
      'fab fa-instagram'
      ]
    })
}
</script>

<style>
   .footer_layout{
       width:100% !important;
   }
</style>
