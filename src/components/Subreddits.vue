<template>
  <div id="wrapper">
    <div id="subreddits">
        <h2>Subreddits</h2>
      <div class="subreddits" v-if="!loading">
        <div
          @click="getPosts(item.data.url)"
          v-for="(item, index) in subreddits"
          :key="index"
        >
          {{ item.data.title }}
        </div>
      </div>
      <div v-else>Loading...</div>
    </div>
    <div id="posts" v-if="posts.length">
        <h2>
            Posts
        </h2>
      <PostItem
        v-for="(item, index) in posts"
        :key="index"
        :title="item.data.title"
      />
    </div>
  </div>
</template>

<script>
import axios from "axios";
import PostItem from "./PostItem";

export default {
  name: "App",
  data() {
    return {
      subreddits: [],
      posts: [],
      loading: true,
    };
  },

  components: {
    PostItem,
  },

  async created() {
    this.subreddits = await this.fetchData().then(function (res) {
      return res.data.data.children;
    });
    this.loading = false;
  },

  methods: {
    fetchData() {
      return axios.get("https://www.reddit.com/subreddits.json");
    },

    async getPosts(url) {
      this.posts = await axios
        .get(`https://www.reddit.com/${url}.json?limit=10`)
        .then(function (res) {
          return res.data.data.children;
        });
      console.log(this.posts);
    },
  },
};
</script>

<style scoped lang="scss">
#wrapper {
  display: flex;
  width: 100%;

  #subreddits,
  #posts {
    width: 50%;
    border: 1px solid lightgray;
  }
}
</style>
