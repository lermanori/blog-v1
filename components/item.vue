<template>
  <v-layout justify-center style="min-height:25vh; max-height:80vh;">
    <v-card style="width:100%" :color="color" dark>
      <v-card-title class="py-1">
        <v-layout align-center justify-space-between row fill-height>
          <span
            id="card-title"
            class="black--text pt-1"
            style="font-size:3vw;"
          >{{`ARTISTS OF TEL AVIV - ISSUE N.${issue}`}}</span>
          <div>
            <v-btn
              class="mx-0"
              :style="{transform:'translateY(8px)'}"
              :disabled="i == (buttons-Index)"
              icon
              v-for="i in buttons"
              :key="i"
              @click="control(i)"
            >
              <v-icon
                v-ripple
                style="transform:translateY(-5px)"
                :size="$vuetify.breakpoint.mdAndUp ? '48':'24'"
              >fiber_manual_record</v-icon>
            </v-btn>
          </div>
        </v-layout>
      </v-card-title>
      <v-img :aspect-ratio="21/9" class="mx-2 mb-2" :src="src">
        <v-layout class="pb-1" align-end justify-space-between row fill-height>
          <v-flex xs8 class="ml-2">
            <h6 class="myfont" style="font-size:3vw">MEET THE ARTIST OF THE WEEK</h6>
            <h3 class="myfont" style="font-size:6vw;font-weight:1000;line-height:4.7vw;">{{name}}</h3>
            <div>
              <h6
                class="myfont"
                :style="{'font-size':'3vw',
                         'overflow-wrap': 'break-word',
                         'max-width': '50vw'}"
              >{{body.split(" ").slice(0,12).toString()+'...'}}</h6>
            </div>
          </v-flex>
          <v-btn class="yellow black--text mb-1 ml-3" style="height:5vw;">
            <span class="myfont" style="font-size:3vw;font-weight:1000;">SEE ALL</span>
          </v-btn>
        </v-layout>
      </v-img>
    </v-card>
  </v-layout>
</template>

<script>
export default {
  data: function() {
    return {};
  },
  props: ["color", "index", "name", "body", "issue", "src", "buttons"],
  methods: {
    control(i) {
      if (i == 1) this.$emit("new");
      if (i == 2) this.$emit("mid");
      if (i == 3) this.$emit("oldest");
    }
  },
  computed: {
    Index() {
      return this.index;
    }
  }
};
</script>

<style scoped>
#hero {
  font-size: 60px;
  color: #f7cade;
  font-family: myriad-hebrew, sans-serif;
  font-style: normal;
  font-weight: 800;
  line-height: 55px;
}
#card-title {
  font-family: myriad-hebrew, sans-serif;
  font-style: bold;
  font-weight: 800;
  /*font-size: 10px;*/
}
.my-font {
  font-family: myriad-hebrew, sans-serif;
  font-style: bold;
}
</style>
