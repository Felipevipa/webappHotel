<template>
  <h1> Working consulta por fecha</h1>
  <input type="date" id="fecha" v-model="fecha" min="2018-01-01" max="2030-12-31">
  <button v-on:click="buscar()"> Buscar </button>
</template>

<script>
import axios from "axios";

export default {
  name: "consultarFecha",
  data() {
    return {
      todos: null,
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
        this.listarResDate = result.data.data.listarResDate;
        console.log(this.listarResDate)
      } catch (error) {
        console.error(error);
      }
    },
  }
}
</script>

<style scoped>

</style>