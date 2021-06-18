<template>
  <v-container>
    <v-card width="500">
      <v-card-title>
        <h1>Zmiana hasła</h1>
      </v-card-title>

      <v-card-text>
        <v-form>
          <v-text-field
            v-model="newPassword"
            :type="showNewPassword ? 'text' : 'password'"
            label="Nowe hasło"
            prepend-icon="mdi-lock"
            :append-icon="showNewPassword ? 'mdi-eye-off' : 'mdi-eye'"
            required
            @click:append="showNewPassword = !showNewPassword"
          />

          <v-text-field
            v-model="currentPassword"
            :type="showCurrentPassword ? 'text' : 'password'"
            label="Stare hasło"
            prepend-icon="mdi-lock"
            :append-icon="showCurrentPassword ? 'mdi-eye-off' : 'mdi-eye'"
            required
            @click:append="showCurrentPassword = !showCurrentPassword"
          />
        </v-form>
      </v-card-text>

      <v-card-actions class="d-flex justify-end">
        <v-btn color="primary" @click="changePassword">Zmień hasło</v-btn>
      </v-card-actions>
    </v-card>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue'

export default Vue.extend({
  name: 'AdminManager',
  data: () => ({
    newPassword: '',
    showNewPassword: false,
    currentPassword: '',
    showCurrentPassword: false,
  }),
  methods: {
    changePassword() {
      console.log(this.newPassword, this.currentPassword)
    },
  },
})
</script>
