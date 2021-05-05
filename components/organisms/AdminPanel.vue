<template>
  <v-app id="inspire">
    <v-navigation-drawer v-model="drawer" app>
      <v-list>
        <v-list-item link @click="currentPanel = 0">
          <v-list-item-icon>
            <v-icon>mdi-logout</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>Menadżer testów</v-list-item-title>
          </v-list-item-content>
        </v-list-item>

        <v-list-item link @click="currentPanel = 1">
          <v-list-item-icon>
            <v-icon>mdi-logout</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>Zarządzaj panelem</v-list-item-title>
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

    <v-main class="pt-2 ml-2">
      <ExamManager v-if="currentPanel === 0" />
      <AdminManager v-else-if="currentPanel === 1" />
    </v-main>
  </v-app>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  data: () => ({
    drawer: null,
    currentPanel: 0,
  }),
})
</script>
