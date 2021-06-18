<template>
  <v-card v-if="answers.length">
    <v-card-title>
      <h3>Pytanie {{ currentQuestion }}/{{ questionsLength }}</h3>
    </v-card-title>

    <v-card-text>
      {{ questions[currentQuestionIndex].question }}

      <v-divider></v-divider>

      <v-form>
        <!-- single -->
        <v-radio-group
          v-if="questions[currentQuestionIndex].type === 'single'"
          v-model="answers[currentQuestionIndex].answer"
        >
          <v-radio
            v-for="(answer, i) in questions[currentQuestionIndex].answers"
            :key="i"
            :label="answer"
            :value="i"
          ></v-radio>
        </v-radio-group>

        <!-- multi -->
        <v-container
          v-if="questions[currentQuestionIndex].type === 'multi'"
          fluid
        >
          <v-checkbox
            v-for="(answer, i) in questions[currentQuestionIndex].answers"
            :key="i"
            v-model="answers[currentQuestionIndex].answer"
            :label="answer"
            :value="i"
            hide-details="auto"
          ></v-checkbox>
        </v-container>

        <!-- text -->
        <v-col
          v-if="questions[currentQuestionIndex].type === 'text'"
          cols="12"
          md="6"
        >
          <v-textarea
            v-model="answers[currentQuestionIndex].answer"
            solo
            label="Odpowiedź"
          ></v-textarea>
        </v-col>
      </v-form>
    </v-card-text>

    <v-card-actions class="d-flex justify-space-between">
      <div>
        <v-btn v-if="!isTheFirst" color="primary" @click="--currentQuestion">
          Powrót
        </v-btn>

        <v-btn v-if="isTheLast" color="primary" @click="submitAnswers">
          Wyślij
        </v-btn>

        <v-btn v-else color="primary" @click="++currentQuestion"> Dalej </v-btn>
      </div>

      <v-col cols="2">
        <v-select
          v-model="currentQuestion"
          label="Idź do pytania"
          :items="items"
        ></v-select>
      </v-col>
    </v-card-actions>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'QuizQuestion',
  data: () => ({
    currentQuestion: 1,
    questions: [
      {
        id: 'i8y773lsy45f4c25',
        question: 'First question',
        type: 'single',
        answers: ['first', 'second', 'third', 'fourth'],
      },
      {
        id: 'nzg4sa5g9rx3akdw',
        question: 'Second question',
        type: 'multi',
        answers: ['abc', 'def', 'ghi', 'jkl'],
      },
      {
        id: '8nex1sxein7btuhf',
        question: 'Third question',
        type: 'text',
      },
    ],
    answers: [] as object[],
  }),
  computed: {
    questionsLength(): number {
      return this.questions.length
    },
    currentQuestionIndex(): number {
      return this.currentQuestion - 1
    },
    items(): number[] {
      // array from 1 to n
      return [...Array.from({ length: this.questionsLength }).keys()].map(
        (i) => i + 1
      )
    },
    isTheLast(): boolean {
      return this.currentQuestion === this.questionsLength
    },
    isTheFirst(): boolean {
      return this.currentQuestion === 1
    },
  },
  mounted() {
    // my hope is that this code is so awful I'm never allowed to write array of objects logic again.
    for (const [i, question] of this.questions.entries()) {
      this.answers.push({
        id: this.questions[i].id,
        answer: undefined,
      })

      if (question.type === 'multi') {
        // @ts-expect-error
        this.answers[i].answer = []
      }
    }
  },
  methods: {
    submitAnswers() {
      console.log(this.answers)
    },
  },
})
</script>
