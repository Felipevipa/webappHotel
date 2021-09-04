<template>
<div>
<div id="contenedor">
  <h1>LOGIN:</h1>
  <label for="username">Username</label> <br/>
  <input type="text" id="username" v-model="username"> <br/>
  <label for="password">Password:</label> <br/>
  <input type="text" id="password" v-model="password"> <br/>
  <button id="boton" v-on:click="autenticar()"> Login </button>
  <br/>
  <p v-if="resultado">Refresh: {{resultado.refresh}}</p>
  <p v-if="resultado">Access: {{resultado.access}}</p>
</div>
<footer id="contacto">
    <div class="contenedor footer-content">
      <div class="contact-us">
        <h2 class="brand">Hotel G6</h2>
      </div>
      <div class="social-media">
        <a href="./">
          <img class="social-media-icon" src="https://cdn-icons-png.flaticon.com/512/1384/1384017.png">
        </a>
        <a href="./" >
          <img class="social-media-icon" src="https://image.flaticon.com/icons/png/512/2168/2168281.png">
        </a>
        <a href="./">
          <img class="social-media-icon" src="https://image.flaticon.com/icons/png/512/2168/2168302.png">
        </a>
            </div>
        </div>
    </footer>
    </div>
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

#contenedor{
    background: #ffdd90;
    width: 360px;
    height: 360px;
    border-radius: 10px;
    margin: auto;
    margin-top: 50px;
    margin-bottom: 50px;
    padding-top: 60px;
    text-align: center;
    font-size: 20px;
}
#boton{
    position: relative;
    top:30px;
    font-size: 15px;
}
  footer{
    background: #df9f0a;
    padding: 10px;
}

.footer-content{
    display:flex;
    justify-content: space-between; /*Los elementos se pongan uno al lado del otro, pero en las esquinas*/
    align-items: center;
    flex-wrap: wrap;
}

.contact-us{
    width:40%;
    color: #fff;
}

.brand{
    font-weight: 500;
    font-size: 40px;
}

.brand+p{
    /*El hermano de brand que en este caso es parrafo*/
    font-weight: 200;
}

.social-media{
    width:50%;
    display:flex;
    justify-content: flex-end; /*Para que lo ponga al final del contenedor*/
}

.social-media-icon{
    display: inline-block;
    margin-left: 20px;
    width: 60px;
    height: 60px;
    border: 1px solid #fff;
    border-radius: 50%;
    text-align: center;
    color: #fff;
}

.social-media-icon:hover{
    background: #fff;
    color: #df9f0a;
}

.social-media-icon i{
    font-size: 30px;
    line-height: 60px;
}
</style>