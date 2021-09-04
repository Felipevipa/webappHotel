<template>
<div id="reservaDNI">
  <header class="header">
    <img id="icono" src="https://image.flaticon.com/icons/png/512/3114/3114248.png">
  </header>
  <h1> Consultar reserva por DNI:</h1>
  <input type="number" id="dni" v-model="dni">
  <button v-on:click="buscar()"> Buscar </button>
  <div id="info">
  <table class="table table-striped table-bordered">
    <thead>
    <tr>
      <th>Numero Reservacion</th>
      <th>Numero Habitacion</th>
      <th>Cedula del cliente</th>
      <th>FechaReservacion</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="reserva in reservaciones" v-bind:key="reserva">
      <td>{{reserva.numeroRervacion}}</td>
      <td>{{reserva.numeroHabitacion}}</td>
      <td>{{reserva.dni}}</td>
      <td>{{reserva.fechaReservacion}}</td>
      <td><button v-on:click="eliminar(reserva.numeroRervacion)" class="bg-danger"> Elminar </button></td>
    </tr>
    </tbody>
  </table>
  <img src="https://images.unsplash.com/photo-1496417263034-38ec4f0b665a?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=751&q=80">
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
  name: "ReservacionPorDni",
  data() {
    return {
      reservaciones: [],
      dni: 123456,
    }
  },
  methods: {
    async buscar() {
      try {
        var result = await axios({
          method: "POST",
          url: 'https://apihotelg6.herokuapp.com',
          data: {
            query: `
          query Query($listarResClienteDni: Int!) {
              listarResCliente(dni: $listarResClienteDni) {
                numeroRervacion
                numeroHabitacion
                dni
                fechaReservacion
              }
            }
            `, variables: {"listarResClienteDni": this.dni}
          }
        });
        this.reservaciones = result.data.data.listarResCliente;
        console.log(this.reservaciones)
      } catch (error) {
        console.error(error);
      }
    },
    async eliminar(numReserva) {
      try {
        var result = await axios({
          method: "POST",
          url: 'https://apihotelg6.herokuapp.com',
          data: {
            query: `
                  mutation Mutation($eliminarReservaNumeroRervacion: Int!) {
                      eliminarReserva(numeroRervacion: $eliminarReservaNumeroRervacion) {
                        numeroRervacion
                        numeroHabitacion
                        dni
                        fechaReservacion
                      }
                    }
            `, variables: {"eliminarReservaNumeroRervacion": numReserva}
          }
        });
        this.resultado = result.data.data.eliminarReserva;
        console.log(this.resultado)
        alert('Reserva eliminada')
      } catch (error) {
        alert('Reserva no encontrada')
      }
    },
    }
  }
</script>

<style scoped>
#info{
  margin:20px;
  padding:20px;
}
#icono{
    position:absolute;
    top:0px;
    left:30px;
    width:80px;
    height:80px;
    padding: 10px;
    z-index:2;
    border-radius: 20px;
}

#reservaDNI{
  background:#ffdd90;
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