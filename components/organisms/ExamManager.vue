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

      <v-card-actions class="d-flex align-center">
        <v-btn color="primary">
          Nowy test
          <v-icon right> mdi-plus </v-icon>
        </v-btn>

        <v-text-field
          hide-details
          prepend-icon="mdi-magnify"
          single-line
          class="pt-0 mt-0 shrink ml-2"
        ></v-text-field>
      </v-card-actions>
    </v-card>

    <v-row>
      <v-col v-for="n in 24" :key="n" cols="5" xs="1">
        <v-card height="200"></v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'ExamManager',
})
</script>
