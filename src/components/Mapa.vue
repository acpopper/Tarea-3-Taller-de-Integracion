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
  mounted() {
    mapboxgl.accessToken = this.accessToken;

    new mapboxgl.Map({
      container: "mapContainer",
      style: "mapbox://styles/mapbox/streets-v11",
      center: [-70.640698, -33.445043],
      zoom: 8,
    });
  },
  
};
</script>

<style scoped>
.basemap {
  width: 800px;
  height: 400px;
  padding: 30px;
}
</style>