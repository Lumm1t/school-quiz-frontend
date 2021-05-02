<template>
  <v-card width="700" class="mx-auto mt-5">
    <v-card-title class="pb-0">
      <h3>1/1 - pytanie</h3>
    </v-card-title>

    <v-divider></v-divider>

    <v-card-text>
      <p>{{ radios || 'null' }}</p>

      <v-radio-group v-model="radios" mandatory>
        <v-radio label="Radio 1" value="radio-1"></v-radio>
        <v-radio label="Radio 2" value="radio-2"></v-radio>
        <v-radio label="Radio 3" value="radio-3"></v-radio>
        <v-radio label="Radio 4" value="radio-4"></v-radio>
      </v-radio-group>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  name: 'QuizQuestion',
  data() {
    return {
      radios: [],
    }
  },
}
</script>
