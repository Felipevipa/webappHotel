<template>
  <div v-if="!listarHabitacion" class="home">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <header class="header">
        <img id="icono" src="https://image.flaticon.com/icons/png/512/3114/3114248.png">
    </header>

    <section>
        <div id="container">
            <ul  class="slider">
                <li id="slider1">
                    <img src= "https://images.unsplash.com/photo-1529290130-4ca3753253ae?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=755&q=80">
                </li>
                <li id="slider2">
                    <img src="https://images.unsplash.com/photo-1618773928121-c32242e63f39?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=750&q=80">
                </li>

                <li id="slider3">
                    <img src="https://images.unsplash.com/photo-1462539405390-d0bdb635c7d1?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=793&q=80"> 
                </li>
                <li id="slider4">
                    <img src="https://images.unsplash.com/photo-1551632436-cbf8dd35adfa?ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&ixlib=rb-1.2.1&auto=format&fit=crop&w=751&q=80"> 
                </li>
            </ul>
            <ul class="control">
                <!--Contiene el control de las imagenes de arriba-->
                <li> <a href="#slider1"> Piscina</a> </li>
                <li> <a href="#slider2"> Habitaciones</a></li>
                <li> <a href="#slider3"> Bar</a></li>
                <li> <a href="#slider4"> Comedor</a></li>
            </ul>
        </div>
    </section>
    <h2>¿Quíenes somos?</h2>
    <div id="hotel">
        <p>
            Somos un hotel que ofrece la mejor gastronomía de la región,
            contamos con servicio a la habitación, piscina, bar, zona de 
            spa, entre otros servicios para disfrutar en familia, pareja 
            o individual. 
        </p>
    </div>
    <h2>Habitaciones disponibles</h2>

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
<style scoped>
.home{
  background:#ffdd90;
}

.header{
  margin:60px;
}

#cuenta{
    position:absolute;
    top:20px;
    right:30px;
    font-size: 15px;
    padding: 10px;
    border-radius: 4px;
    border:#df9f0a;
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



/*Imagenes*/
#container{
    margin:auto;
    width: 1024px;
    padding: 40px;
}

.control a{ 
    float:left;
    margin-right:100px;
    list-style: none;
    text-decoration: none;
    font-size: 18px;
    color: #126169;
    font-family: 'Orelega One', cursive;
}

ul, li {
    list-style: none;
}
.slider{
    height: 500px;
    width: 1024px;
    position: relative;
}
.slider li{
    position: absolute;
    top:0;
    left: 0;
    opacity: 0; 
    width: inherit; 
    height: inherit;
}

.slider li img{
    width: 100%;
    height: 500px;
    object-fit: cover;
}
.slider li:first-child{
    opacity: 100%; 
}
.slider li:target{
    opacity: 1;
}
h2{
  margin:50px;
  padding:50px;
}
#hotel{
    margin:auto;
    padding: 50px;
    text-align: justify;
    flex-wrap: wrap;
    font-size: 20px;
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