<template>
  <div>
    <v-navigation-drawer v-model="drawer" app>
      <v-list>
        <v-list-item v-for="(link, i) in links" :key="i" link :to="link.link">
          <v-list-item-icon>
            <v-icon>{{ link.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ link.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar app>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-toolbar-title>Admin panel</v-toolbar-title>

      <v-spacer></v-spacer>

      <ThemeBtn />
    </v-app-bar>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data: () => ({
    drawer: undefined,
    links: [
      {
        title: 'Menadżer testów',
        icon: 'mdi-note-search',
        link: '/admin',
      },
      {
        title: 'Zarządzaj panelem',
        icon: 'mdi-account-cog',
        link: '/admin/settings',
      },
    ],
  }),
})
</script>
