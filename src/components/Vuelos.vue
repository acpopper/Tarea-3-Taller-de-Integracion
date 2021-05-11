<template>
  <div :key="vuelo.code" v-for="vuelo in vuelos">
    <Vuelo :vuelo="vuelo" />

  </div>
</template>

<script>
import Vuelo from './Vuelo'
export default {
  name: 'Vuelos',
  props: {
    vuelos: Array,
  },
  components: {
    Vuelo
  }
}
</script>