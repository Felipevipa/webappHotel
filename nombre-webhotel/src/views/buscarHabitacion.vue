<template>
<div class="buscarH">
  <header class="header">
    <img id="icono" src="https://image.flaticon.com/icons/png/512/3114/3114248.png">
  </header>
  <h1> CONSULTAR HABITACION</h1>
  <label for="habitacion">Numero de Habitacion:</label>
  <input type="number" id="habitacion" v-model="habitacion">
  <button v-on:click="buscar()"> Buscar </button>
  <div id="info">
  <table class="table table-striped table-bordered">
      <thead>
      <tr>
        <th>Tipo</th>
        <th>Numero</th>
        <th>Precio</th>
      </tr>
      </thead>
      <tbody>
      <tr v-if="resultado != null">
        <td>{{resultado.numeroHabitacion}}</td>
        <td>{{resultado.precio}}</td>
        <td>{{resultado.tipoHabitacion}}</td>
        <td><button v-on:click="eliminar(resultado.numeroHabitacion)" class="bg-danger"> Eliminar </button></td>
      </tr>
      </tbody>
    </table>
    <img :src= "resultado.imagen" alt="" style="height : 600px">
    </div>
    <footer id="contacto">
      <div class="contenedor footer-content">
        <div class="contact-us">
          <h2 class="brand">Hotel G6</h2>
        </div>
        <div class="social-media">
          <a href="./">
            <img class="social-media-icon" src="https://cdn-icons-png.flaticon.com/512/1384/1384017.png">
          </a>
          <a href="./" >
            <img class="social-media-icon" src="https://image.flaticon.com/icons/png/512/2168/2168281.png">
          </a>
          <a href="./">
            <img class="social-media-icon" src="https://image.flaticon.com/icons/png/512/2168/2168302.png">
          </a>
              </div>
          </div>
      </footer>
    </div>
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
    async eliminar(habitacion) {
      alert(habitacion)
    },
  }
}
</script>

<style scoped>
#info{
  margin:20px;
  padding:20px;
}
#icono{
    position:absolute;
    top:0px;
    left:30px;
    width:80px;
    height:80px;
    padding: 10px;
    z-index:2;
    border-radius: 20px;
}

.buscarH{
  background:#ffdd90;
}
  footer{
    background: #df9f0a;
    padding: 10px;
}

.footer-content{
    display:flex;
    justify-content: space-between; /*Los elementos se pongan uno al lado del otro, pero en las esquinas*/
    align-items: center;
    flex-wrap: wrap;
}

.contact-us{
    width:40%;
    color: #fff;
}

.brand{
    font-weight: 500;
    font-size: 40px;
}

.brand+p{
    /*El hermano de brand que en este caso es parrafo*/
    font-weight: 200;
}

.social-media{
    width:50%;
    display:flex;
    justify-content: flex-end; /*Para que lo ponga al final del contenedor*/
}

.social-media-icon{
    display: inline-block;
    margin-left: 20px;
    width: 60px;
    height: 60px;
    border: 1px solid #fff;
    border-radius: 50%;
    text-align: center;
    color: #fff;
}

.social-media-icon:hover{
    background: #fff;
    color: #df9f0a;
}

.social-media-icon i{
    font-size: 30px;
    line-height: 60px;
}

</style>