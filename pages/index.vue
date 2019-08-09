<template>
  <v-container fluid class="px-0">
    <v-layout justify-center style="min-height:30vh">
      <h1 id="hero" class="mt-5 text-xs-center">THE CITY OF XXX</h1>
    </v-layout>
    <template v-if="Artist_Arr.length > 0">
      <app-carousel :arr="Artist_Arr" />
    </template>
    <app-carousel :arr="NightLife_Arr" v-if="NightLife_Arr.length > 0" />
    <app-carousel :arr="Fashion_Arr" v-if="Fashion_Arr.length > 0" />
  </v-container>
</template>

<script>
import item from "../components/item.vue";
import carousel from "../components/carousel.vue";
import { async } from "q";
export default {
  data: function() {
    return {
      opened: false,
      toggle_exclusive: true,
      transitions: {
        enter_class_left: "animated fadeInLeft",
        enter_class_right: "animated fadeInRight",
        leave_class_left: "animated fadeOutLeft",
        leave_class_right: "animated fadeOutRight"
      },
      enter_active_class: "animated fadeInLeft",
      leave_active_class: "animated fadeOutLeft",
      arr: [
        {
          color: "indigo",
          name: "bad-revolution",
          body: `Lorem ipsum dolor sit amet, consectetur adipiscing elit. Donec sed nisi nulla. Donec blandit in lectus vel semper. Quisque luctus nibh eget mauris pulvinar ultricies. Integer interdum, ex sed ornare vehicula, diam enim finibus mi, non scelerisque nunc odio nec orci. Donec felis nisi, dictum sed porttitor non, vehicula pellentesque urna. Duis id pharetra elit. Morbi placerat turpis eros, id facilisis dui iaculis a. Donec pharetra condimentum ante nec iaculis. Sed eget augue sit amet augue elementum ultricies. Ut tempus purus ornare, lobortis velit sit amet, convallis lectus. Suspendisse potenti. Proin vestibulum eget lorem vel ornare. Morbi sed tempus turpis, at congue sem.
Curabitur interdum augue in est lacinia malesuada. Pellentesque vehicula neque ut interdum lobortis. Praesent ipsum ipsum, accumsan at interdum vel, venenatis a nulla. Ut ullamcorper vehicula ex ac scelerisque. Vivamus aliquet scelerisque ante, sit amet facilisis ex viverra ut. Sed dictum nibh a urna commodo, at cursus nunc placerat. Nulla sit amet vestibulum ex, eget varius risus. Integer pharetra ante id est convallis laoreet. Integer nec laoreet arcu.
Morbi tincidunt sollicitudin orci et consectetur. Etiam nibh erat, efficitur quis quam sed, maximus sollicitudin neque. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Suspendisse non sapien est. Mauris et dapibus lorem. Morbi pharetra eu velit sit amet tristique. Ut auctor arcu quis sem interdum, et congue leo elementum. Integer vulputate sit amet nulla eget pretium. Curabitur vel mi eu nisl congue feugiat. Nam id est suscipit magna finibus scelerisque. Pellentesque habitant morbi tristique senectus et netus et malesuada fames ac turpis egestas. Praesent aliquet lobortis tellus a scelerisque. Maecenas ornare interdum lectus a consectetur. Pellentesque vitae eros fermentum, consectetur risus sed, sodales ligula.`,
          issue: 1,
          src: "https://picsum.photos/200/300"
        }
      ],
      artists_arr: [],
      nightlife_arr: [],
      fashion_arr: [],

      baseURL:
        process.env.DEPLOY_ENV === "GH_PAGES"
          ? "http://strapi-rest-api.herokuapp.com"
          : "http://localhost:1337"
    };
  },
  asyncData(context) {
    return context.app.$storyapi
      .get("cdn/stories", {
        version: "draft",
        starts_with: "page/"
      })
      .then(res => {
        return {
          posts: res.data.stories.map(post => {
            return {
              color: post.content.preview_color,
              name: post.content.Title,
              body: post.content.preview_text,
              issue: post.content.issue_number,
              src: post.content.body[0].image,
              id: post.slug,
              type: post.content.type
            };
          })
        };
      });
  },

  computed: {
    Arr: function() {
      return this.arr;
    },
    Artist_Arr: function() {
      return this.artists_arr;
    },
    NightLife_Arr: function() {
      return this.nightlife_arr;
    },
    Fashion_Arr: function() {
      return this.fashion_arr;
    }
  },
  methods: {},
  components: { "app-carousel": carousel },
  created: async function() {
    this.artists_arr = this.posts.filter(post => post.type == "artist");
    this.nightlife_arr = this.posts.filter(post => post.type == "nightlife");
    this.fashion_arr = this.posts.filter(post => post.type == "fashion");
  }
};
</script>
<style scoped>
</style>

