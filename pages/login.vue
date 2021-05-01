<template>
  <div>
    <v-form @submit="onSubmit">
      <v-container>
        <h2 class="text-center">Login</h2>
        <v-row>
          <v-col cols="12" sm="2"> </v-col>
          <v-col cols="12" sm="8">
            <v-text-field
              v-model="email"
              type="email"
              label="Email"
            ></v-text-field>
            <v-text-field
              v-model="password"
              type="password"
              label="Password"
            ></v-text-field>
            <v-btn color="primary" type="submit">Login</v-btn>

            <v-alert
              v-show="error"
              class="mt-2 text-center"
              border="top"
              color="red lighten-2"
              dark
            >
              Invalid password
            </v-alert>
          </v-col>
          <v-col cols="12" sm="2"> </v-col>
        </v-row>
      </v-container>
    </v-form>
  </div>
</template>

<script>
export default {
  middleware: 'isLoggedIn',
  data() {
    return {
      email: '',
      password: '',
      error: null,
    }
  },
  methods: {
    async onSubmit(e) {
      e.preventDefault()

      const payload = {
        data: {
          email: this.email,
          password: this.password,
        },
      }

      try {
        await this.$auth.loginWith('local', payload)
        this.$router.push('/')
      } catch (error) {
        this.error = error
      }
    },
  },
}
</script>

<style scoped>
.txtfield {
  width: 50%;
}
</style>
