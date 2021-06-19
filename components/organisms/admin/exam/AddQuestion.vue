<template>
  <v-card>
    <v-card-title>
      <h1>Dodaj pytanie</h1>
    </v-card-title>

    <v-card-text>
      <h2>Treść pytania:</h2>
      <v-col class="d-flex" cols="12" sm="8">
        <TextEditor v-model="newQuestion.title" class="my-5" />
      </v-col>

      <h2>Typ odpowiedzi:</h2>
      <v-col class="d-flex" cols="12" sm="6">
        <v-select
          v-model="newQuestion.type"
          :items="questionTypes"
          filled
          single-line
          @change="resetCorrectAnswer"
        ></v-select>
      </v-col>

      <h2>Odpowiedzi:</h2>
      <v-btn color="primary" text @click="newQuestion.answers.push('')">
        Dodaj odpowiedź
      </v-btn>

      <!-- single & multi -->
      <div
        v-if="
          newQuestion.type === 'Jednokrotny wybór' ||
          newQuestion.type === 'Wielokrotny wybór'
        "
      >
        <v-col class="d-flex flex-column" cols="12" sm="8">
          <div v-for="i in answersLength" :key="i">
            <h4>Odpowiedź {{ i }}</h4>
            <v-btn
              color="error"
              small
              @click="newQuestion.answers.splice(i - 1, 1)"
            >
              Usuń
            </v-btn>

            <TextEditor v-model="newQuestion.answers[i - 1]" class="my-5" />
          </div>
        </v-col>

        <div v-if="newQuestion.type === 'Jednokrotny wybór'">
          <h2>Poprawna odpowiedź:</h2>
          <v-col cols="2">
            <v-select
              v-model="newQuestion.correctAnswer"
              :items="answersToSelect"
              single-line
            ></v-select>
          </v-col>
        </div>

        <div v-else-if="newQuestion.type === 'Wielokrotny wybór'">
          <h2>Poprawna odpowiedź:</h2>
          <v-col cols="2">
            <v-select
              v-model="newQuestion.correctAnswer"
              :items="answersToSelect"
              multiple
              single-line
            ></v-select>
          </v-col>
        </div>
      </div>

      <!-- text -->
      <v-col
        v-if="newQuestion.type === 'Krótka odpowiedź'"
        class="d-flex flex-column"
        cols="12"
        sm="8"
      >
        <div v-for="i in answersLength" :key="i">
          <h4>Odpowiedź {{ i }}</h4>
          <v-btn
            color="error"
            small
            @click="newQuestion.answers.splice(i - 1, 1)"
          >
            Usuń
          </v-btn>

          <TextEditor v-model="newQuestion.correctAnswer[i - 1]" class="my-5" />
        </div>
      </v-col>
    </v-card-text>

    <v-card-actions>
      <v-btn color="primary" @click="addNewQuestion">Dodaj</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'AddQuestion',
  data: () => ({
    newQuestion: {
      title: '',
      type: 'Jednokrotny wybór',
      answers: ['', '', ''],
      correctAnswer: 0 as number | number[],
    },
    questionTypes: [
      'Jednokrotny wybór',
      'Wielokrotny wybór',
      'Krótka odpowiedź',
    ],
  }),
  computed: {
    answersLength(): number {
      return this.newQuestion.answers.length
    },
    answersToSelect(): number[] {
      // array from 1 to n
      return [...Array.from({ length: this.answersLength }).keys()].map(
        (i) => i
      )
    },
  },
  methods: {
    resetCorrectAnswer() {
      this.newQuestion.answers = ['', '', '']
      this.newQuestion.correctAnswer = []
    },
    addNewQuestion() {
      console.log(this.newQuestion)
    },
  },
})
</script>
