<template>
  <v-container>
    <v-card width="600">
      <v-card-title>
        <h1>Nowy test</h1>
      </v-card-title>

      <v-card-text>
        Dane podstawowe

        <v-divider></v-divider>

        <v-form>
          <v-text-field
            v-model="examName"
            label="Nazwa testu"
            prepend-icon="mdi-account-circle"
            required
          />

          <v-text-field
            v-model="examDescription"
            label="Opis testu"
            prepend-icon="mdi-account-circle"
            required
          />
        </v-form>
      </v-card-text>

      <v-card-actions>
        <v-btn color="primary" @click="createNewQuiz">Utwórz</v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'ExamNew',
  data: () => ({
    examName: '',
    examDescription: '',
  }),
  methods: {
    createNewQuiz() {
      console.log(this.examName, this.examDescription)

      this.$router.push(`/admin/exams/${this.examName}`) // will be exam id, not name
    },
  },
})
</script>
