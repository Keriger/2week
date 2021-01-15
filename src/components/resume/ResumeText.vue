<template>
  <p v-html="text">
  </p>
</template>

<script>
export default {
  name: 'ResumeText',
  props: {
    text: {
      type: String
    }
  }
}
</script>

<style scoped>

</style>
