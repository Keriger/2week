<template>
    <ul class="list">
      <li class="list-item">
        <div>
          <p><strong>{{ email }}</strong></p>
          <small>{{ body }}</small>
        </div>
      </li>
    </ul>
</template>

<script>
export default {
  name: 'CommentList',
  props: {
    email: {
      type: String
    },
    body: {
      type: String
    }
  }
}

</script>

<style scoped>

</style>
