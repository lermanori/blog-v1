<template>
  <div>
    <div class="px-4 py-4">
      <div class="ma-3 pa-1" style="background-color:gray;position:fixed;top:0;right:0; ">
        <h3>ISSUE NU.{{header.issueNumber}}</h3>
      </div>
      <h2 style="color:pink">MEET THE {{header.type.toUpperCase()}} OF THE WEEK</h2>
      <h1
        style="color:yellow;font-size:42px;font-weight:800;margin:0px"
      >{{header.name.toUpperCase()}}</h1>
      <h4 style="color:pink">{{header.preview_text}}</h4>
    </div>
    <div v-for="(post,index) in posts" :key="index">
      <div class="post-thumbnail" :style="{backgroundImage: 'url(' + post.image +')'}"></div>
      <div class="pa-4">
        <div v-html="$md.render(post.text)" />
      </div>
    </div>
  </div>
</template>

<style  scoped>
.post-thumbnail {
  width: 100%;
  height: 300px;
  background-size: cover;
  background-position: center;
}

div {
  color: pink;
}

div >>> em {
  color: yellow;
  font-style: normal;
}
</style>

<script>
export default {
  asyncData(context) {
    return context.app.$storyapi
      .get("cdn/stories/page/" + context.params.postId, {
        version: "draft"
      })
      .then(result => {
        return {
          posts: result.data.story.content.body,
          header: {
            name: result.data.story.content.Title,
            preview_text: result.data.story.content.preview_text,
            issueNumber: result.data.story.content.issue_number,
            type: result.data.story.content.type
          }
        };
      })
      .catch(err => {
        console.log(err);
      });
  },
  mounted() {
    this.$storybridge.on("change", () => {
      location.reload(true);
    });
  }
};
</script>


