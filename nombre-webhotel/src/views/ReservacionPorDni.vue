<template>
  <h1> Working consulta por dni</h1>
  <input type="number" id="dni" v-model="dni">
  <button v-on:click="buscar()"> Buscar </button>
  <table class="table table-striped table-bordered">
    <thead>
    <tr>
      <th>numeroReservacion</th>
      <th>Numero Habitacion</th>
      <th>Cedula del cliente</th>
      <th>fechaReservacion</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="reserva in reservaciones" v-bind:key="reserva">
      <td>{{reserva.numeroRervacion}}</td>
      <td>{{reserva.numeroHabitacion}}</td>
      <td>{{reserva.dni}}</td>
      <td>{{reserva.fechaReservacion}}</td>
    </tr>
    </tbody>
  </table>
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
    }
  }
</script>

<style scoped>

</style>