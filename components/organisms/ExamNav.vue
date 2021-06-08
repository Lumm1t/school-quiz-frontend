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
  data() {
    return {
      drawer: undefined,
      links: [
        {
          title: 'Ustawienia wstępne',
          icon: 'mdi-note-search',
          link: (this as any).getLink('basic-settings'),
        },
        {
          title: 'Menadżer pytań',
          icon: 'mdi-account-cog',
          link: (this as any).getLink('question-manager'),
        },
        {
          title: 'Parametry czasowe',
          icon: 'mdi-account-cog',
          link: (this as any).getLink('time-parameters'),
        },
        {
          title: 'Dostęp do testu',
          icon: 'mdi-account-cog',
          link: (this as any).getLink('test-access'),
        },
        {
          title: 'Wyniki',
          icon: 'mdi-account-cog',
          link: (this as any).getLink('exam-results'),
        },
      ],
    }
  },
  methods: {
    getLink(link: string) {
      return `/admin/exams/${this.$route.params.slug}/${link}`
    },
  },
})
</script>
