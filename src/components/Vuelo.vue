<template>
  <div @click="mostrarPasajeros()" class="vuelo">
    <h3>
      {{ vuelo.airline }}
    </h3>
    <p>{{vuelo.plane}}: {{vuelo.code}}</p>
    <p>Seats: {{vuelo.seats}}</p>
    <p>From: {{vuelo.origin}}</p>
    <p>To: {{vuelo.destination}}</p>
    <h5>Click for passengers</h5>
    
  </div>
</template>

<script>
export default {
  name: 'Vuelo',
  props: {
    vuelo: Object,
  },
  methods: {
    mostrarPasajeros() {
      var texto= ''
      texto += 'Name | Age\n'
      var i;
      for (i = 0; i < this.vuelo.passengers.length; i++) {
        texto += this.vuelo.passengers[i].name + " | "+ this.vuelo.passengers[i].age + "\n";
      }
      window.alert('*Passengers* \n' + texto)
      texto = ''
    }
  }
}
</script>

<style scoped>
.vuelo {
  background: #f4f4f4;
  margin: 5px;
  padding: 5px 20px;
  cursor: pointer;
}
.vuelo h3 {
  font-size: 20px;
  align-items: center;
  justify-content: space-between;
}
p {
  font-size: 14px;
}
</style>