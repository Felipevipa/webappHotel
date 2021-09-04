<template>
  <h1> Working consulta por dni</h1>
  <input type="number" id="habitacion" v-model="habitacion">
  <button v-on:click="buscar()"> Buscar </button>
  <table class="table table-striped table-bordered">
      <thead>
      <tr>
        <th>Tipo</th>
        <th>Numero</th>
        <th>Precio</th>
        <th>Imagen</th>
      </tr>
      </thead>
      <tbody>
      <tr v-if="resultado != null">
        <td>{{resultado.numeroHabitacion}}</td>
        <td>{{resultado.precio}}</td>
        <td>{{resultado.tipoHabitacion}}</td>
        <td> <img :src="resultado.imagen" alt="" style="height : 200px"> </td>
      </tr>
      </tbody>
    </table>
</template>

<script>
import axios from "axios";

export default {
  name: "buscarHabitacion",
  data() {
    return {
      resultado: null,
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
        this.resultado = result.data.data.mostrarInfoHab;
        console.log(this.resultado)
      } catch (error) {
        alert('Habitacion no encontrada')
      }
    },
  }
}
</script>

<style scoped>

</style>