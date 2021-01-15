<template>
  <h2 v-text="subtitle"></h2>
</template>

<script>
export default {
  name: 'ResumeSubtitle',
  props: {
    subtitle: {
      type: String
    }
  }

}
</script>

<style scoped>

</style>
