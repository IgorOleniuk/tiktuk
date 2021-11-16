<template>
  <section>
    <div class="feeds_block_body">
      <div class="feeds_block_body__video-block">
        <video controls>
          <source src="https://www.w3schools.com/html/mov_bbb.mp4" type="video/mp4">
          Your browser does not support the video tag.
        </video>
      </div>
      <p>{{ feed.desc }}</p>
      <div class="feeds_block_body__details">
        <details v-if="feed.authorStats">
          <summary>Feed info:</summary>
          <p>{{ feed.stats.playCount }} times was watched</p>
          <p>{{ feed.stats.shareCount }} times was shared</p>
          <p>{{ feed.stats.commentCount }} comments</p>
        </details>
        <details v-else>
          <summary>Feed info:</summary>
          <p>{{ feed.playCount }} times was watched</p>
          <p>{{ feed.shareCount }} times was shared</p>
          <p>{{ feed.commentCount }} comments</p>
        </details>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'UserFeed',

  props: {
    feed: {
      type: Object,
      required: true
    }
  }
}
</script>
