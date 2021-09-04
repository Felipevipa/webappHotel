<template>
  <h1> Working consulta por fecha</h1>
  <input type="date" id="fecha" v-model="fecha" min="2018-01-01" max="2030-12-31">
  <button v-on:click="buscar()"> Buscar </button>
  <table class="table table-striped table-bordered">
    <thead>
    <tr>
      <th>numeroReservacion</th>
      <th>Numero Habitacion</th>
      <th>Identificacion del cliente</th>
      <th>fechaReservacion</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="reserva in todos" v-bind:key="reserva">
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
  name: "consultarFecha",
  data() {
    return {
      todos: [],
      fecha: "2022-07-28",
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
          query Query($listarResDateFechaReservacion: LocalDate!) {
                listarResDate(fechaReservacion: $listarResDateFechaReservacion) {
                  numeroRervacion
                  numeroHabitacion
                  dni
                  fechaReservacion
                }
              }
            `, variables: {"listarResDateFechaReservacion": this.fecha}
          }
        });
        this.todos = result.data.data.listarResDate;
        console.log(this.todos)
      } catch (error) {
        console.error(error);
      }
    },
  }
}
</script>

<style scoped>

</style>