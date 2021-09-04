<template>
  <h1>LOGIN:</h1>
  <label for="username">Username</label> <br/>
  <input type="text" id="username" v-model="username"> <br/>
  <label for="password">Password:</label> <br/>
  <input type="text" id="password" v-model="password"> <br/>
  <button v-on:click="autenticar()"> Login </button>
  <br/>
  <p v-if="resultado">Refresh: {{resultado.refresh}}</p>
  <p v-if="resultado">Access: {{resultado.access}}</p>

</template>

<script>
import axios from "axios";

export default {
  name: "crearReserva",
  data() {
    return {
      resultado: null,
      username: '',
      password: ''
    }
  },
  methods: {
    async autenticar() {
      try {
        var result = await axios({
          method: "POST",
          url: 'https://apihotelg6.herokuapp.com',
          data: {
            query: `
                  mutation Mutation($authenticateCredentials: CredentialsInput!) {
                    authenticate(credentials: $authenticateCredentials) {
                      refresh
                      access
                    }
                  }
            `, variables: {
              "authenticateCredentials": {
                "username":this.username,
                "password":this.password
              }
            }
          }
        });
        this.resultado = result.data.data.authenticate;
        console.log(this.resultado)
        alert('Autenticado')
        this.$router.push({ name: 'Home' })
      } catch (error) {
        alert('No autenticado')
      }
    },

  }
}
</script>

<style scoped>

</style>