<template>
  <div></div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  layout: 'admin-exam',
  beforeCreate() {
    this.$router.push(`/admin/exams/${this.$route.params.slug}/basic-settings`)
  },
})
</script>
