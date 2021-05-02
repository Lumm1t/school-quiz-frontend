<template>
  <v-btn icon @click="switchTheme()">
    <v-icon>mdi-brightness-6</v-icon>
  </v-btn>
</template>

<script>
export default {
  name: 'ThemeBtn',
  methods: {
    switchTheme() {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark
    },
  },
}
</script>
