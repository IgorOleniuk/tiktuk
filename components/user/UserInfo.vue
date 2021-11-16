<template>
  <section class="section-block user-section">
    <div class="user-profile-block">
      <b-avatar class="user-profile-block__avatar" :src="userInfo.user.avatarLarger"></b-avatar>
    </div>
    <div class="user-profile-block user-profile-block__info">
      <h2>{{ userInfo.user.nickname }}</h2>
      <div class="user-profile-block__info__stat">
        <p>Followers: {{ userInfo.stats.followerCount }}</p>
        <p>Following: {{ userInfo.stats.followingCount }}</p>
        <p>Digg count: {{ userInfo.stats.diggCount }}</p>
        <p>Heart count: {{ userInfo.stats.heartCount }}</p>
        <p>Videos: {{ userInfo.stats.videoCount }}</p>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  props: {
    userInfo: {
      type: Object,
      required: true
    }
  }
}
</script>
