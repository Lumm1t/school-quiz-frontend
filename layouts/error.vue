<template>
  <v-app>
    <h1 v-if="error.statusCode === 404">
      {{ pageNotFound }}
    </h1>
    <h1 v-else>
      {{ otherError }}
    </h1>

    <NuxtLink to="/">Strona główna</NuxtLink>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  layout: 'empty',
  props: {
    error: {
      type: Object,
      default: undefined,
    },
  },
  data: () => ({
    pageNotFound: '404 Not Found',
    otherError: 'An error occurred',
  }),
  head() {
    const title =
      this.error.statusCode === 404 ? this.pageNotFound : this.otherError

    return {
      title,
    }
  },
})
</script>

<style scoped>
h1 {
  font-size: 20px;
}
</style>
