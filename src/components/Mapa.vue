<template>
  <div id="mapContainer" class="basemap"></div>
</template>

<script>
import mapboxgl from "mapbox-gl";

export default {
  name: "Mapa",
  data() {
    return {
      accessToken: "pk.eyJ1IjoiYWNwb3BwZXIiLCJhIjoiY2twMHRjN2ptMHZqMjJ2cHJ4N3pyZ2EyZCJ9.IiAVirZxsxsvJFQIdGf3hg",
    };
  },
  props: {
    posiciones: Array

  },
  methods: {
    actualizar(map) {
      this.posiciones.forEach(function (marker) {
      // Add markers to the map.
      new mapboxgl.Marker()
      var correct = [marker.position[1], marker.position[0]]
      // console.log(correct)
      .setLngLat(correct)
      // we
      .addTo(map);
      });
    }
  },
  mounted() {
    mapboxgl.accessToken = this.accessToken;
    const map = new mapboxgl.Map({
      container: "mapContainer",
      style: "mapbox://styles/mapbox/streets-v11",
      center: [-70.640698, -33.445043],
      zoom: 8,
    });
    this.actualizar(map)
  },
  
};

</script>

<style scoped>
.basemap {
  width: 800px;
  height: 400px;
  padding: 30px;
}
.marker {
  height: 25px;
  width: 25px;
  background-color: #bbb;
  
  display: inline-block;
}
</style>