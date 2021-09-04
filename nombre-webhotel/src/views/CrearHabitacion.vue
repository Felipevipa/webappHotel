<template>
  <h1>CREAR HABITACION:</h1>
  <label for="numero">Numero de habitacion: </label> <br/>
  <input type="number" id="numero" v-model="numero"> <br/>
  <label for="precio">Precio: </label> <br/>
  <input type="number" id="precio" v-model="precio"> <br/>
  <label>Tipo de habitacion</label> <br/>
  <select v-model="selected" id="tipoH">
    <option disabled value="">Seleccione un elemento</option>
    <option>Sencilla</option>
    <option>Doble</option>
    <option>Familiar</option>
  </select> <br/>
  <button v-on:click="crear()"> Crear </button>
</template>

<script>
import axios from "axios";

export default {
  name: "CrearHabitacion",
  data() {
    return {
      resultado: null,
      numero: 1,
      precio: 0,
      selected: '',
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
                  mutation Mutation($crearHabitacionHabitacion: habitacionnueva!) {
                    crearHabitacion(habitacion: $crearHabitacionHabitacion) {
                      numeroHabitacion
                      precio
                      tipoHabitacion
                      imagen
                    }
                  }
            `, variables: {
              "crearHabitacionHabitacion" : {
                "numeroHabitacion": this.numero,
                "precio": this.precio,
                "tipoHabitacion": this.selected
              }
            }
          }
        });
        this.resultado = result.data.data.crearHabitacion;
        console.log(this.resultado)
        alert('Habitacion creada')
      } catch (error) {
        alert('Habitacion no encontrada')
      }
    },
  }
}
</script>

<style scoped>

</style>