<template>
<div>
<div id="contenedor">
  <h1>CREAR RESERVA:</h1>
  <label for="numero">Numero de Habitacion</label> <br/>
  <input type="number" id="numero" v-model="numero"> <br/>
  <label for="dni">DNI:</label> <br/>
  <input type="number" id="dni" v-model="dni"> <br/>
  <label for="fecha"> Fecha </label> <br/>
  <input type="date" id="fecha" v-model="fecha" min="2018-01-01" max="2030-12-31">
  <button id="boton" v-on:click="crear()"> Crear </button>
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
      numero: 1,
      dni: 0,
      fecha: "2022-07-28",
    }
  },
  methods: {
    async crear() {
      try {
        var result = await axios({
          method: "POST",
          url: 'https://apihotelg6.herokuapp.com',
          data: {
            query: `
                  mutation EliminarReservaMutation($crearReservaReserva: nuevaReserva!) {
                    crearReserva(reserva: $crearReservaReserva) {
                      numeroRervacion
                      numeroHabitacion
                      dni
                      fechaReservacion
                    }
                  }
            `, variables: {
              "crearReservaReserva": {
                "numeroHabitacion": this.numero,
                "dni": this.dni,
                "fechaReservacion" : this.fecha
              }
            }
          }
        });
        this.resultado = result.data.data.crearReserva;
        console.log(this.resultado)
        alert('Reserva creada')
      } catch (error) {
        alert('Habitacion no encontrada')
      }
    },

  }
}
</script>

<style scoped>
#contenedor{
    background: #ffdd90;
    width: 460px;
    height: 460px;
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
    top:100px;
    border-radius: 5px;
    font-size: 20px;
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