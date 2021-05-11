<template>
  <div class="vuelo">
    <h3>
      {{ vuelo.airline }}
    </h3>
    <p>{{vuelo.plane}}</p>
  </div>
</template>

<script>
export default {
  name: 'Vuelo',
  props: {
    vuelo: Object,
  },
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
  align-items: center;
  justify-content: space-between;
}
</style>