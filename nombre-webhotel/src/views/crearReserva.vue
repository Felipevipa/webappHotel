<template>
  <h1>Working crear reserva...</h1>
  <label for="numero">Numero de Habitacion</label> <br/>
  <input type="number" id="numero" v-model="numero"> <br/>
  <label for="dni">DNI:</label> <br/>
  <input type="number" id="dni" v-model="dni"> <br/>
  <label for="fecha"> Fecha </label> <br/>
  <input type="date" id="fecha" v-model="fecha" min="2018-01-01" max="2030-12-31">
  <button v-on:click="crear()"> Crear </button>
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

</style>