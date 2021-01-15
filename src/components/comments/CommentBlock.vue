<template>
  <div class="container">
    <p>
      <button class="btn primary" @click="getComments">Загрузить комментарии</button>
    </p>

    <div v-show="loaderVisible" v-if="!comments.length" class="loader"></div>

    <div v-else class="card">
      <h2>Комментарии</h2>
      <comment-list
        v-for="(comment, idx) in comments"
        :key="idx"
        :email="comment.email"
        :body="comment.body"
      ></comment-list>
    </div>
  </div>
</template>

<script>
import CommentList from '@/components/comments/CommentList'
import axios from 'axios'

export default {
  name: 'CommentBlock',
  emits: ['get-comments'],
  data () {
    return {
      loaderVisible: false,
      comments: []
    }
  },
  methods: {
    async getComments () {
      this.loaderVisible = true
      const { data } = await axios.get('https://jsonplaceholder.typicode.com/comments?_limit=42')
      this.comments = data
      this.loaderVisible = false
    }
  },
  components: {
    CommentList
  }
}
</script>

<style scoped>

</style>
