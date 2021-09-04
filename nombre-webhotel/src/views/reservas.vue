<template>
  <h1>reservas working.</h1>

  <table class="table table-striped table-bordered">
    <thead>
    <tr>
      <th>numeroReservacion</th>
      <th>Numero</th>
      <th>dni</th>
      <th>fechaReservacion</th>
    </tr>
    </thead>
    <tbody>
    <tr v-for="reserva in reservas" v-bind:key="reserva">
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
  name: "reservas",
  data() {

    return {
      reservas: null
    }
  },
  async mounted() {
    try {
      var result = await axios({
        method: "POST",
        url: 'https://apihotelg6.herokuapp.com',
        data: {
          query: `
          {
                listarReserva {
                  numeroRervacion
                  numeroHabitacion
                  dni
                  fechaReservacion
                }
                }
            `
        }
      });
      this.reservas = result.data.data.listarReserva;
      console.log(this.reservas)
    } catch (error) {
      console.error(error);
    }
  },

}
</script>

<style scoped>

</style>