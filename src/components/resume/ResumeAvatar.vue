<template>
  <div class="avatar">
    <img alt="avatar" :src="avatar">
  </div>
</template>

<script>
export default {
  name: 'ResumeAvatar',
  props: {
    avatar: {
      type: String
    }
  }
}
</script>

<style scoped>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
