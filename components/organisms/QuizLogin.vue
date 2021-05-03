<template>
  <v-card width="500" class="mx-auto mt-5">
    <v-card-title class="pb-0">
      <h1>School quiz</h1>
    </v-card-title>

    <v-divider></v-divider>

    <v-card-text>
      Podaj imię, nazwisko oraz kod dostępu.

      <v-form>
        <v-text-field
          v-model="firstName"
          label="Imię"
          prepend-icon="mdi-account-circle"
          required
        />

        <v-text-field
          v-model="lastName"
          label="Nazwisko"
          prepend-icon="mdi-account-circle"
          required
        />

        <v-text-field
          v-model="accessCode"
          :type="showAccessCode ? 'text' : 'password'"
          label="Kod dostępu"
          prepend-icon="mdi-lock"
          :append-icon="showAccessCode ? 'mdi-eye-off' : 'mdi-eye'"
          required
          @click:append="showAccessCode = !showAccessCode"
        />
      </v-form>
    </v-card-text>

    <v-card-actions>
      <v-btn color="info">Rozpocznij</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'QuizLogin',
  data: () => ({
    showAccessCode: false,
    firstName: '',
    lastName: '',
    accessCode: '',
  }),
})
</script>
