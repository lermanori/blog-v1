<template>
  <v-container fluid class="px-0">
    <v-layout row wrap justify-center class="mb-4">
      <v-flex xs12 class="text-xs-center">
        <h1 id="hero">{{title.first}}</h1>
      </v-flex>
      <v-flex xs12 class="text-xs-center">
        <h1 id="hero">{{title.second}}</h1>
      </v-flex>
    </v-layout>
    <v-layout align-center justify-center>
      <nuxt-link :to="posts[0].id" style="text-decoration:none;">
        <v-img
          contains
          :src="posts[0].img_src"
          aspect-ratio="1"
          class="grey lighten-2 mx-5 mt-5"
          max-width="500"
          max-height="300"
        >
          <h1 class="white--text pl-2" id="issuenum">ISSUE NU. {{posts[0].issueNumber}}</h1>
          <v-layout column fill-height class="lightbox white--text">
            <v-spacer></v-spacer>
            <div id="img-bottom-container" class="pa-2">
              <h2>MEET THE ARTIST OF THE WEEK</h2>
              <h1>{{posts[0].name}}</h1>
              <p>
                <b>{{posts[0].preview_text}}</b>
              </p>
            </div>
          </v-layout>
        </v-img>
      </nuxt-link>
    </v-layout>
    <v-container fluid grid-list-xl>
      <v-layout row wrap justify-between>
        <template v-for="(artist_post,index) in bricks">
          <v-flex xs6 class :key="index">
            <nuxt-link :to="artist_post.id">
              <v-img :aspect-ratio="1" :src="artist_post.img_src">
                <v-layout column fill-height class="black--text">
                  <v-spacer></v-spacer>
                  <div class="subheading artists-name pl-4">{{artist_post.name}}</div>
                </v-layout>
              </v-img>
            </nuxt-link>
          </v-flex>
        </template>
      </v-layout>
    </v-container>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      title: { first: "THE ARTISTS", second: "OF TEL AVIV" }
    };
  },
  computed: {
    bricks() {
      const [head, ...tail] = this.posts;
      return tail;
    }
  },

  asyncData(context) {
    return context.app.$storyapi
      .get("cdn/stories", {
        version: "draft",
        starts_with: "page/"
      })
      .then(res => {
        return {
          posts: res.data.stories
            .filter(post => {
              return post.content.type == "artist";
            })
            .map(post => {
              return {
                //color: post.content.preview_color,
                name: post.content.Title,
                preview_text: post.content.preview_text,
                issueNumber: post.content.issue_number,
                img_src: post.content.body[0].image,
                id: post.slug,
                type: post.content.type
              };
            })
        };
      });
  }
};
</script>

<style scoped>
* {
  font-family: myriad-hebrew, sans-serif;
}
#hero {
  font-size: 12vw;
  padding: 0px;
  font-family: myriad-hebrew, sans-serif;
  font-style: bold;
  font-weight: 800;
}
#issuenum {
  font-size: 1em;
  font-family: myriad-hebrew, sans-serif;
  font-style: bold;
  font-weight: 800;
  background-color: rgba(58, 58, 58, 0.747);
}
#img-bottom-container {
  background-color: rgba(58, 58, 58, 0.747);
}
.artists-name {
  background-color: rgba(58, 58, 58, 0.747);
  transform: translateY(12px);
  font-size: 2em;
  font-weight: 800;
}
</style>
