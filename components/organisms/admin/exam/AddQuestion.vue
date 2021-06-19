<template>
  <v-card>
    <v-card-title>
      <h1>Dodaj pytanie</h1>
    </v-card-title>

    <v-card-text>
      <!-- Question title -->
      <h2>Treść pytania:</h2>

      <v-col class="d-flex" cols="12" sm="8">
        <TextEditor v-model="questionTitle" class="my-5" />
      </v-col>

      <!-- Answer type -->
      <h2>Typ odpowiedzi:</h2>
      <v-col class="d-flex" cols="12" sm="6">
        <v-select
          v-model="questionType"
          :items="questionTypes"
          filled
          single-line
        ></v-select>
      </v-col>

      <!-- Question answers -->
      <v-btn color="primary" text @click="++numberOfAnswers">
        Dodaj odpowiedź
      </v-btn>

      <v-btn color="primary" text @click="--numberOfAnswers">
        Usuń odpowiedź
      </v-btn>

      <v-col class="d-flex flex-column" cols="12" sm="8">
        <div v-for="i in numberOfAnswers" :key="i">
          <div v-if="questionType === 'single' || questionType === 'multi'">
            <h4>Odpowiedź {{ i }}</h4>

            <TextEditor v-model="questionAnswers[i - 1]" class="my-5" />
          </div>

          <div v-else-if="questionType === 'text'">
            <h4>Odpowiedź {{ i }}</h4>

            <TextEditor v-model="questionCorrectAnswers[i - 1]" class="my-5" />
          </div>
        </div>
      </v-col>

      <div v-if="questionType === 'single'">
        <h2>Poprawna odpowiedź:</h2>
        <v-col cols="2">
          <v-select
            v-model="questionCorrectAnswers"
            :items="answersToSelect"
            single-line
          ></v-select>
        </v-col>
      </div>
      <div v-else-if="questionType === 'multi'">
        <h2>Poprawne odpowiedzi:</h2>
        <v-col cols="2">
          <v-select
            v-model="questionCorrectAnswers"
            :items="answersToSelect"
            multiple
            single-line
          ></v-select>
        </v-col>
      </div>
    </v-card-text>

    <v-card-actions>
      <v-btn color="primary" @click="addNewQuestion">Dodaj</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue'

interface question {
  title: string
  type: string
  answers?: any[]
  correctAnswers: any[] | number | string
}

export default Vue.extend({
  name: 'AddQuestion',
  data: () => ({
    questionTitle: '',
    questionType: 'single',
    questionAnswers: [],
    questionCorrectAnswers: [],
    questionTypes: ['single', 'multi', 'text'],
    numberOfAnswers: 2,
  }),
  computed: {
    answersToSelect(): number[] {
      // array from 0 to n
      return [...Array.from({ length: this.numberOfAnswers }).keys()]
    },
  },
  watch: {
    questionType() {
      this.questionAnswers = []
      this.questionCorrectAnswers = []
    },
  },
  methods: {
    addNewQuestion() {
      const newQuestion: question = {
        title: this.questionTitle,
        type: this.questionType,
        correctAnswers: this.questionCorrectAnswers,
      }

      if (this.questionType !== 'text')
        newQuestion.answers = this.questionAnswers

      console.log(newQuestion)
    },
  },
})
</script>
