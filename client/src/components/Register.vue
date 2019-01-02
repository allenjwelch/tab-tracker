<template>
  <div class="register">
    <v-layout column>
        <v-flex xs6>
            <div class="white elevation-2">
                <v-toolbar flat dense class='cyan' dark>
                    <v-toolbar-title>Register</v-toolbar-title>
                </v-toolbar>
            </div>
        </v-flex>
    </v-layout>
    <div class='pl-4 pr-4 pt-2 pb-2'>
        <input v-model="email" type="email" name="email" placeholder="Email" />
        <br>
        <input v-model="password" type="password" name="password" placeholder="Password" />
        <br>
        <div class='error' v-html='error'></div>
        <v-btn class="cyan" @click="register">Register</v-btn>
    </div>
  </div>
</template>

<script>
import AuthenticationService from '@/services/AuthenticationService'

export default {
  name: 'Register',
  data () {
    return {
      email: '',
      password: '',
      error: null
    }
  },
  watch: {
    email (value) {
      console.log('email has changed')
    }
  },
  methods: {
    async register() {
        try {
            const response = await AuthenticationService.register({
              email:this.email,
              password: this.password
            })
        } catch (error) {
            this.error = error.response.data.error
        }
      console.log(response.data)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    .error {
        color: red;
    }
</style>
