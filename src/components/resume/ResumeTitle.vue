<template>
  <h1 v-html="title"></h1>
</template>

<script>
export default {
  name: 'ResumeTitle',
  props: {
    title: {
      type: String
    }
  }
}
</script>

<style scoped>

</style>
