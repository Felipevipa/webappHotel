<template>
  <div v-if="!listarHabitacion" class="home">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <p>working home....</p>

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
      <tr v-for="habitacion in todos" v-bind:key="habitacion.numeroHabitacion">
        <td>{{habitacion.tipoHabitacion}}</td>
        <td>{{habitacion.numeroHabitacion}}</td>
        <td>{{habitacion.precio}}</td>
        <td> <img :src="habitacion.imagen" alt="" style="height : 200px"> </td>
      </tr>
      </tbody>
    </table>
  </div>

</template>

<script>

import axios from 'axios'

export default {
  name: 'Home',
  data() {

    return {
      todos: []
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
                    listarHabitacion {
                        tipoHabitacion,
                        numeroHabitacion,
                        precio,
                        imagen
                  }
                }
            `
        }
      });
      this.todos = result.data.data.listarHabitacion;
      console.log(this.todos)
    } catch (error) {
      console.error(error);
    }
  },
}
</script>
