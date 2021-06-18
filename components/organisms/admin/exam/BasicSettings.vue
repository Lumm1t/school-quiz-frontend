<template>
  <v-card width="500">
    <v-card-title>
      <h1>Ustawienia wstępne</h1>
    </v-card-title>

    <v-card-text>
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

    <v-card-actions class="d-flex justify-end">
      <v-btn color="primary" @click="saveBasicSettings">Zapisz</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'BasicSettings',
  data: () => ({
    examName: '',
    examDescription: '',
  }),
  methods: {
    saveBasicSettings() {
      console.log(this.examName, this.examDescription)
    },
  },
})
</script>
