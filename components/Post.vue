<template>
  <section>
    <div v-if="feed.authorMeta" class="feeds_block_header">
      <NuxtLink :to="`/user/${feed.authorMeta.name}`" class="user-info_link">
        <div class="feeds_block_header__avatar-block">
          <b-avatar size="4rem" :src="feed.authorMeta.avatar"></b-avatar>
        </div>
        <h5>{{ feed.authorMeta.nickName }}</h5>
      </NuxtLink>
    </div>
    <div class="feeds_block_body">
      <div class="feeds_block_body__video-block">
        <video controls autoplay>
          <source :src="feed.videoUrl" type="video/mp4">
          Your browser does not support the video tag.
        </video>
      </div>
      <p>{{ feed.text ? feed.text : feed.desc }}</p>
      <div class="feeds_block_body__details">
        <details v-if="feed.authorStats">
          <summary>Feed info:</summary>
          <p>{{ feed.playCount }} times was watched</p>
          <p>{{ feed.shareCount }} times was shared</p>
          <p>{{ feed.commentCount }} comments</p>
        </details>
        <details v-else>
          <summary>Feed info:</summary>
          <p>{{ feed.playCount }} times was watched</p>
          <p>{{ feed.shareCount }} times was shared</p>
          <p>{{ feed.commentCount }} comments</p>
        </details>
        <div class="post-block__tags">
          <details>
            <summary>Tags:</summary>
            <p v-for="tag in feed.hashtags"
               :key="tag.id"
            >
              {{ tag.name }}
            </p>
          </details>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'Post',

  props: {
    feed: {
      type: Object,
      required: true
    }
  }
}
</script>
