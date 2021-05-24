<template>
  <div style="display: flex; align-items:center">
    <div style="text-align: center">
      <Mapa :posiciones="posiciones" />
    </div>
    <h2 style="width: 60px"></h2>
    <div v-show="!loggedIn" style="text-align: center;">
      <Login @name-login="login" />
    </div>
    <div v-show="loggedIn" style="position:relative">
      <div class="chatt" id="myDiv">
        <ul id="messages" style="word-wrap: break-word"></ul>
        <!-- the chat is a feature, not a bug -->
        <Chat @enviar-mensaje="enviarMensaje" style="position: relative; bottom: 0; right: 0;"/>
      </div>
    </div>
  
  </div>
  
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
import Chat from './components/Chat'
import Vuelos from './components/Vuelos'
import Login from './components/Login'
import Mapa from './components/Mapa'

const io = require("socket.io-client");

const socket = io("wss://tarea-3-websocket.2021-1.tallerdeintegracion.cl",
 {path: '/flights'});



export default {
  name: 'App',
  components: {
    BotonInfo,
    Vuelos,
    Chat,
    Login,
    Mapa
  },
  methods: {
    mostrarVuelos() {
      socket.emit('FLIGHTS')
      this.showVuelos = true
    },
    enviarMensaje(msg) {
      socket.emit('CHAT', {name: this.nombre, message: msg});
    },
    login(nombre) {
      this.loggedIn = true,
      this.nombre = nombre
    },
    actualizar(vuelo) {
      this.posiciones.unshift(vuelo)
      this.posiciones = this.posiciones.filter((thing, index, self) => 
      self.findIndex(t => t.code === thing.code) === index)
    }

  },
  
  data() {
    return {
      vuelos: [],
      showVuelos: false,
      isConnected: false,
      loggedIn: false,
      nombre: '',
      posiciones: []
    }
  },
  created() {
    socket.on('FLIGHTS', (vls) => {this.vuelos=vls;}),

    socket.on('CHAT', (msg) => {
      var messages = document.getElementById('messages');
      var item = document.createElement('li')
      item.textContent = msg.name + ': ' + msg.message
      messages.appendChild(item)
      var myDiv = document.getElementById("myDiv")
      myDiv.scrollTop = myDiv.scrollHeight
      var date = new Date(msg.date).toLocaleTimeString().replace(/([\d]+:[\d]{2})(:[\d]{2})(.*)/, "$1$3")
      console.log(date)
      ;}),

    socket.on('POSITION', (pos) => {
      this.actualizar(pos)
      // console.log(this.posiciones)
      ;})
    
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
.chatt {
  position:relative;
  align-items: center;
  width: 500px;
  margin: 10px auto;
  overflow-y: auto;
  height: 300px;
  border: 2px solid rgb(70, 154, 180);
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
  #messages { list-style-type: none; margin: 0; padding: 0;}
  #messages > li { padding: 0.5rem 1rem; }
  #messages > li:nth-child(odd) { background: #efefef; }
</style>
