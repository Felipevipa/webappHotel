<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/ReservacionPorDni">Consultar reserva</router-link> |
    <router-link to="/buscarHabitacion">Consultar habitacion</router-link> |
    <router-link to="/consultarFecha">Consultar Fecha</router-link> |
    <router-link to="/crearReserva">Crear Reserva</router-link> |
    <router-link to="/CrearHabitacion">Crear Habitacion</router-link> |
    <router-link to="/reservas">Reservas</router-link> |
    <router-link to="/about">Login</router-link>
  </div>
  <router-view/>
  <p>Working vueapp...</p>



</template>

<script>

</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
  background:#ffdd90;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
