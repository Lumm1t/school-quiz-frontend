<template>
  <v-card>
    <v-card-title>
      <h3>Pytanie {{ currentQuestion }}/{{ questionsLength }}</h3>
    </v-card-title>

    <v-card-text>
      {{ questions[currentQuestion - 1].question }}

      <v-divider></v-divider>

      <v-form>
        <p>{{ answers[currentQuestion - 1] || 'null' }}</p>

        <v-radio-group v-model="answers[currentQuestion - 1]">
          <v-radio
            v-for="(answer, i) in questions[currentQuestion - 1].answers"
            :key="i"
            :label="answer"
            :value="currentQuestion - 1 + `-` + i"
          ></v-radio>
        </v-radio-group>
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
        question: 'First question',
        answers: ['first', 'second', 'third', 'fourth'],
      },
      {
        question: 'Second question',
        answers: ['abc', 'def', 'ghi', 'jkl'],
      },
      {
        question: 'Third question',
        answers: ['Aurora', 'Allison', 'Alexis', 'Ava'],
      },
    ],
    answers: [],
  }),
  computed: {
    questionsLength(): number {
      return this.questions.length
    },
    items(): number[] {
      // array from 1 to n
      return [...Array(this.questionsLength).keys()].map((i) => i + 1)
    },
    isTheLast(): boolean {
      return this.currentQuestion === this.questionsLength
    },
    isTheFirst(): boolean {
      return this.currentQuestion === 1
    },
  },
  methods: {
    submitAnswers() {
      console.log(this.answers)
    },
  },
})
</script>
