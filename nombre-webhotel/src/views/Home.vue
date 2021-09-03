<template>
  <div class="home">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <p>working home...</p>

    <table>
      <tr>
        <td>Tipo</td>
        <td>Numero</td>
        <td>Precio</td>
        <td>Imagen</td>
      </tr>

      <tr v-for="habitacion in listarHabitacion" v-bind:key="habitacion">
        <td v-for="item in habitacion" v-bind:key="item">
          {{ item }} <br/>
        </td>
      </tr>
      <tr v-for="habitacion in listarHabitacion" v-bind:key="habitacion">
        <td> {{ habitacion[0] }}</td>
        <td> {{ habitacion[1] }}</td>
        <td> {{ habitacion[2] }}</td>
        <td> {{ habitacion[3] }}</td>
      </tr>
    </table>
  </div>

</template>

<script>

import axios from 'axios'

export default {
  name: 'Home',
  data() {
    return {
      todos: null
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
      this.listarHabitacion = result.data.data.listarHabitacion;
      console.log(this.listarHabitacion)
    } catch (error) {
      console.error(error);
    }
  },
}
</script>
