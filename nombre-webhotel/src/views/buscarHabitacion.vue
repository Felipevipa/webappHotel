<template>
  <h1> Working consulta por dni</h1>
  <input type="number" id="habitacion" v-model="habitacion">
  <button v-on:click="buscar()"> Buscar </button>
</template>

<script>
import axios from "axios";

export default {
  name: "buscarHabitacion",
  data() {
    return {
      todos: null,
      habitacion: 1,
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
          query Query($mostrarInfoHabNumeroHabitacion: Int!) {
                mostrarInfoHab(numeroHabitacion: $mostrarInfoHabNumeroHabitacion) {
                  numeroHabitacion
                  precio
                  tipoHabitacion
                  imagen
                }
              }
            `, variables: {"mostrarInfoHabNumeroHabitacion": this.habitacion}
          }
        });
        this.mostrarInfoHab = result.data.data.mostrarInfoHab;
        console.log(this.mostrarInfoHab)
      } catch (error) {
        console.error(error);
      }
    },
  }
}
</script>

<style scoped>

</style>