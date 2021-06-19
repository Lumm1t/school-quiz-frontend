<template>
  <v-card>
    <v-card-title>
      <h1>Parametry czasowe</h1>
    </v-card-title>

    <v-card-text>
      Limit czasowy na każde pytanie występujące w teście (podany w sekundach):

      <v-text-field
        v-model="questionAnswerTime"
        style="width: 100px"
        type="number"
      ></v-text-field>
    </v-card-text>

    <v-card-actions>
      <v-btn color="primary" @click="saveQuestionAnswerTime">Zapisz</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'TimeParameters',
  data: () => ({
    questionAnswerTime: 60,
  }),
  methods: {
    saveQuestionAnswerTime() {
      console.log(this.questionAnswerTime)
    },
  },
})
</script>
