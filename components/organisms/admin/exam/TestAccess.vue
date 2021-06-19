<template>
  <v-card>
    <v-card-title>
      <h1>Dostęp do testu</h1>
    </v-card-title>

    <v-card-subtitle class="mt-1">
      Dostęp do testu będzie możliwy tylko dzięki znajomości indywidualnego kodu
      dostępu.
    </v-card-subtitle>

    <v-card-text>
      Aktualne kody dostępu dla tego testu: {{ currentCodes.join(', ') }}
    </v-card-text>

    <v-card-actions>
      <v-dialog v-model="dialog" width="300">
        <template #activator="{ on, attrs }">
          <v-btn color="primary" dark v-bind="attrs" v-on="on">
            Wygeneruj kod
          </v-btn>
        </template>

        <v-card>
          <v-card-title class="text-h5"> Nowy kod dostępu </v-card-title>

          <v-card-text>p8fyal</v-card-text>

          <v-divider></v-divider>

          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="primary" text @click="dialog = false"> Ok </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
      <v-btn color="error">Zablokuj dostęp</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'TestAccess',
  data: () => ({
    dialog: false,
    currentCodes: ['zlv8z0', 'wojbqq'],
  }),
  methods: {},
})
</script>
