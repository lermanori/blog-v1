<template>
  <v-app dark style="background-color:black">
    <v-layout row wrap class="text-xs-center" style="max-height:5vh;">
      <v-btn
        @click="dialog=!dialog"
        fab
        small
        class="ma-3 pa-2"
        color="yellow"
        style="position:fixed;top:0;left:0;z-index:5;"
      ></v-btn>
    </v-layout>
    <v-content>
      <v-container class="mt-4 px-0">
        <nuxt v-if="!dialog" />
        <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition">
          <v-card>
            <v-toolbar dark color="pink lighten-4">
              <v-btn icon dark @click="dialog = false">
                <v-icon>close</v-icon>
              </v-btn>
            </v-toolbar>
            <v-layout row wrap justify-center>
              <v-flex xs12 class="text-xs-center ma-3">
                <nuxt-link class="main-link" to="/artists">
                  <h1 @click="dialog = false">ARTISTS</h1>
                </nuxt-link>
              </v-flex>
              <v-flex xs12 class="text-xs-center ma-3">
                <nuxt-link class="main-link" to="/fashion">
                  <h1 @click="dialog = false">FASHION</h1>
                </nuxt-link>
              </v-flex>
              <v-flex xs12 class="text-xs-center ma-3">
                <nuxt-link class="main-link" to="/nightlife">
                  <h1 @click="dialog = false">NIGHTLIFE</h1>
                </nuxt-link>
              </v-flex>
              <v-flex xs12 class="text-xs-center mb-3">
                <nuxt-link class="main-link" to="/">
                  <v-icon color="pink lighten-4" large @click="dialog = false">home</v-icon>
                </nuxt-link>
              </v-flex>
            </v-layout>
          </v-card>
        </v-dialog>
      </v-container>
    </v-content>
  </v-app>
</template>

<script>
export default {
  data() {
    return {
      dialog: false,
      notifications: false,
      sound: true,
      widgets: false
    };
  }
};
</script>
<style>
* {
  box-sizing: border-box;
}
body {
  font-family: myriad-hebrew, sans-serif;
}
a {
  text-decoration: none;
}
.main-link {
  color: #f8bbd0;
}
</style>
