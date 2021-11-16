<template>
  <b-container>
    <UserInfo v-if="userData" :userInfo="userData" />

    <section v-if="feeds && userData" class="section-block feeds_block">
      <h2 class="">Posts:</h2>
      <div
        v-for="feed in paginatedFeeds"
        :key="feed.id"
        class="posts-block"
      >
        <UserFeed :feed="feed" />
      </div>
      <b-pagination
        v-model="currentPage"
        :per-page="perPage"
        :total-rows="totalRows"
        size="lg"
        class="feed-paginator"
      ></b-pagination>
    </section>
  </b-container>
</template>

<script>
import UserInfo from '../../components/user/UserInfo';
import UserFeed from '../../components/user/UserFeed';
import userFeeds from 'static/user-feed.json';

export default {
  components: {
    UserInfo,  UserFeed
  },

  data () {
    return {
      userData: null,
      feeds: null,
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
    this.feeds = userFeeds.itemList;
    console.log(this.feeds);
    this.getUserData();

    this.$nextTick(() => {
      this.$nuxt.$loading.start()
    })
  },

  methods: {
    getUserData () {
      this.$axios.get(`user/info/${this.$route.params.slug}`)
        .then((res) => {
          console.log(res)
          if (!res.data) {
            this.getUserData();
            this.$nextTick(() => {
              this.$nuxt.$loading.start()
            })
          }
          this.userData = res.data;

          this.$nuxt.$loading.finish()
        }).catch((err) => {
        console.log(err);
      })
    },

    /*getUserFeeds () {
      this.$axios.get(`user/feed/${this.$route.params.slug}`)
        .then((res) => {
          this.feeds = res.data;

          // this.$nuxt.$loading.finish()
        }).catch((err) => {
        console.log(err);
      })
    }*/

  }
}
</script>
