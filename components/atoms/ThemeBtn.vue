<template>
  <v-tooltip bottom>
    <template #activator="{ on }">
      <v-btn icon @click="changeTheme" v-on="on">
        <v-icon>mdi-brightness-6</v-icon>
      </v-btn>
    </template>

    <span>Zmień Tło</span>
  </v-tooltip>
</template>

<script>
import { mapMutations } from 'vuex'
import setupTheme from '@/assets/setupTheme'

export default {
  name: 'ThemeBtn',
  mounted() {
    setupTheme.call(this)
  },
  methods: mapMutations(['changeTheme']),
}
</script>
