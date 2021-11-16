<template>
  <section v-if="feeds.length" class="section-block feeds_block">
    <h2>Latest Feeds:</h2>
    <!--  posts  -->
    <div
      v-for="feed in paginatedFeeds"
      :key="feed.id"
      class="posts-block"
    >
      <Post :feed="feed" />
    </div>
    <b-pagination
      v-model="currentPage"
      :per-page="perPage"
      :total-rows="totalRows"
      size="lg"
      class="feed-paginator"
    ></b-pagination>
  </section>
</template>

<script>
import Post from './Post';

export default {
  name: 'TrendingFeed',

  components: {
    Post
  },

  data () {
    return {
      feeds: [],
      perPage: 5,
      currentPage: 1,
    }
  },

  computed: {
    paginatedFeeds () {
      const items = this.feeds;
      // Return just page of items needed
      return items.slice(
        (this.currentPage - 1) * this.perPage,
        this.currentPage * this.perPage
      )
    },
    totalRows () {
      return this.feeds.length;
    }
  },

  mounted () {
    this.$nextTick(() => {
      this.getLatestFeeds();
      this.$nuxt.$loading.start()
    })
  },

  methods: {
    getLatestFeeds () {
      this.$axios.get('/trending/feed')
            .then((res) => {
              this.$nuxt.$loading.finish()
               this.feeds = res.data;
              console.log( this.feeds);
            }).catch((err) => {
              console.log(err);
            })
    }
  }
}
</script>
