<template>
  <div>
    <v-card class="mb-5">
      <v-card-title>
        <h1>Menadżer pytań</h1>
      </v-card-title>

      <v-card-text>
        Witaj w Menedżerze pytań! W tym miejscu możesz tworzyć i edytować
        pytania do stworzonego testu.
      </v-card-text>

      <v-card-actions class="d-flex flex-wrap">
        <v-btn color="primary" to="./question-manager/add-question">
          Dodaj pytanie
          <v-icon right> mdi-plus </v-icon>
        </v-btn>
      </v-card-actions>
    </v-card>

    <v-card
      v-for="(question, i) in questions"
      :key="i"
      width="800"
      class="my-5"
    >
      <v-card-title>
        <h1 class="text-h6">Pytanie {{ i + 1 }}</h1>
      </v-card-title>

      <v-card-text>
        {{ question.question }}

        <!-- single -->
        <v-radio-group v-if="question.type === 'single'" disabled>
          <v-radio
            v-for="(answer, i) in question.answers"
            :key="i"
            :label="answer"
            :value="i"
            :style="
              question.correctAnswer === i ? 'background-color: lightgreen' : ''
            "
            class="pa-1"
          ></v-radio>
        </v-radio-group>

        <!-- multi -->
        <v-container v-if="question.type === 'multi'">
          <v-checkbox
            v-for="(answer, i) in question.answers"
            :key="i"
            :label="answer"
            :value="i"
            class="ma-0 pa-1"
            hide-details="auto"
            :style="
              question.correctAnswer.includes(i)
                ? 'background-color: lightgreen'
                : ''
            "
            disabled
          ></v-checkbox>
        </v-container>

        <!-- text -->
        <div
          v-if="question.type === 'text'"
          class="pa-1 mt-3"
          style="background-color: lightgreen"
        >
          Możliwe odpowiedzi: {{ [...question.correctAnswer].join(', ') }}
        </div>
      </v-card-text>

      <v-card-actions>
        <v-tooltip bottom>
          <template #activator="{ on }">
            <v-btn class="mx-2" fab small outlined color="warning" v-on="on">
              <v-icon dark>mdi-pencil</v-icon>
            </v-btn>
          </template>

          <span>Edytuj</span>
        </v-tooltip>

        <v-tooltip bottom>
          <template #activator="{ on }">
            <v-btn class="mx-2" fab small outlined color="primary" v-on="on">
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
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'QuestionManager',
  data: () => ({
    currentQuestion: 1,
    questions: [
      {
        id: 'i8y773lsy45f4c25',
        question: 'First question',
        type: 'single',
        answers: ['first', 'second', 'third', 'fourth'],
        correctAnswer: 1,
      },
      {
        id: 'nzg4sa5g9rx3akdw',
        question: 'Second question',
        type: 'multi',
        answers: ['abc', 'def', 'ghi', 'jkl'],
        correctAnswer: [0, 3],
      },
      {
        id: '8nex1sxein7btuhf',
        question: 'Third question',
        type: 'text',
        correctAnswer: ['car', 'auto', 'truck'],
      },
    ],
  }),
})
</script>
