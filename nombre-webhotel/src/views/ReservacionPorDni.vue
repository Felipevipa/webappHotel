<template>
  <h1> Working consulta por dni</h1>
  <input type="number" id="dni" v-model="dni">
  <button v-on:click="buscar()"> Buscar </button>
</template>

<script>
import axios from "axios";

export default {
  name: "ReservacionPorDni",
  data() {
    return {
      todos: null,
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
        this.listarResCliente = result.data.data.listarResCliente;
        console.log(this.listarResCliente)
      } catch (error) {
        console.error(error);
      }
    },
    }
  }
</script>

<style scoped>

</style>