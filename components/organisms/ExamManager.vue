<template>
  <v-container>
    <v-card class="mb-5">
      <v-card-title>
        <h1>Menadżer testów</h1>
      </v-card-title>

      <v-card-text>
        Witaj w menedżerze testów! W tym miejscu możesz tworzyć nowe testy oraz
        zarządzać istniejącymi - edytować ich parametry, usuwać je lub
        duplikować.
      </v-card-text>

      <v-card-actions
        class="d-flex flex-wrap"
        :class="{
          'justify-center': $vuetify.breakpoint.smAndDown,
          'justify-start': $vuetify.breakpoint.mdAndUp,
        }"
      >
        <v-btn color="primary" to="/admin/exams-manager/new-exam">
          Nowy test
          <v-icon right> mdi-plus </v-icon>
        </v-btn>

        <v-text-field
          v-model="wantedExams"
          hide-details
          prepend-icon="mdi-magnify"
          single-line
          class="shrink mt-0 pt-0 ml-3"
        ></v-text-field>
      </v-card-actions>
    </v-card>

    <v-row>
      <v-col v-for="(exam, i) in examsToRender" :key="i" cols="12" md="6">
        <v-card height="100%" :to="exam.link">
          <v-card-title>
            <h1>{{ exam.name }}</h1>
          </v-card-title>

          <v-card-text>
            {{ exam.description }}
          </v-card-text>

          <v-card-actions>
            <v-tooltip bottom>
              <template #activator="{ on }">
                <v-btn
                  class="mx-2"
                  fab
                  small
                  outlined
                  color="primary"
                  v-on="on"
                >
                  <v-icon dark>mdi-content-duplicate</v-icon>
                </v-btn>
              </template>

              <span>Duplikuj</span>
            </v-tooltip>

            <v-tooltip bottom>
              <template #activator="{ on }">
                <v-btn class="mx-2" fab small outlined color="error" v-on="on">
                  <v-icon dark>mdi-delete</v-icon>
                </v-btn>
              </template>

              <span>Usuń</span>
            </v-tooltip>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue'

interface Exam {
  name: string
  description: string
  link: string
}

export default Vue.extend({
  name: 'ExamManager',
  data: () => ({
    wantedExams: '' as string,
    allExams: [
      {
        name: 'C# Quiz 1',
        description:
          'Poniżej znajduje się 10 pytań z C#, za pomocą których możesz sprawdzić swoją wiedzę.',
        link: '#',
      },
      {
        name: 'JavaScript - podstawy',
        description: 'Podstawy z języka JS.',
        link: '#',
      },
      {
        name: 'HTML - tagi',
        description: 'Sprawdzian z znaczników HTML.',
        link: '#',
      },
      {
        name: 'CSS - kartkówka',
        description: 'Grid & flexbox',
        link: '#',
      },
    ] as Exam[],
    examsToRender: [] as Exam[],
  }),
  watch: {
    wantedExams(val) {
      this.examsToRender =
        val === ''
          ? [...this.allExams]
          : this.allExams.filter((exam) => exam.name.includes(val))
    },
  },
  mounted() {
    this.examsToRender = [...this.allExams]
  },
})
</script>
