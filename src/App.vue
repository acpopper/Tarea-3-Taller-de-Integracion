<template>

  <div>
    <BotonInfo @toggle-show-vuelos="mostrarVuelos" />
  </div>
  <!-- pequeña nota display:flex; align-items: center; on <row> -->
  <div class="container" style="display: flex" v-show="showVuelos">
    <Vuelos :vuelos="vuelos" />
  </div>
  
  

</template>

<script>
import BotonInfo from './components/BotonInfo'
import Vuelos from './components/Vuelos'
const io = require("socket.io-client");

const socket = io("wss://tarea-3-websocket.2021-1.tallerdeintegracion.cl",
 {path: '/flights'});

export default {
  name: 'App',
  components: {
    BotonInfo,
    Vuelos
  },
  methods: {
    mostrarVuelos() {
      socket.emit('FLIGHTS')
      this.showVuelos = true
    },
  },
  
  data() {
    return {
      vuelos: [],
      showVuelos: false,
      isConnected: false
    }
  },
  created() {
    socket.on('FLIGHTS', (vls) => {this.vuelos=vls;})
    
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: 'Poppins', sans-serif;
}
.container {
  overflow: scroll;
  align-items: center;
  max-width: 80%;
  margin: 10px auto;
  overflow: auto;
  min-height: 100px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: rgb(185, 63, 63);
  color: #fff;
  border: none;
  padding: 10px ;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}

</style>
