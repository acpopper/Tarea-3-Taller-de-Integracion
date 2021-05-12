<template>
<div>
  <p v-if="isConnected">We're connected to the server!</p>
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
import Vuelos from './components/Vuelos'

export default {
  name: 'App',
  components: {
    BotonInfo,
    Vuelos
  },
  methods: {
    mostrarVuelos() {
      this.showVuelos = true
    }
  },
  sockets: {
    connect() {
      // Fired when the socket connects.
      this.isConnected = true;
    },

    disconnect() {
      this.isConnected = false;
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
    this.vuelos = [
      {
        code: 1,
        airline: 'American Airlines',
        origin: [1.1, 1.2],
        destination: [10.1, 10.2],
        plane: 'Model x',
        seats: 100,
        passengers: [{name: 'Alan', age: 25},
        {name: 'Dennis', age: 23}]
      },
      {
        code: 2,
        airline: 'United',
        origin: [2.1, 2.2],
        destination: [20.1, 20.2],
        plane: 'Model y',
        seats: 200,
        passengers: [{name: 'Pony', age: 25},
        {name: 'Salvaje', age: 23}]
      },
      {
        code: 3,
        airline: 'Lufthansa',
        origin: [3.1, 3.2],
        destination: [30.1, 30.2],
        plane: 'Model z',
        seats: 300,
        passengers: [{name: 'Johnny', age: 25},
        {name: 'Bravo', age: 23}]
      }
    ]
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
