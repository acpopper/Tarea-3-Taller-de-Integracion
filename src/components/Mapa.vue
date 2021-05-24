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
    posiciones: Object
  },
  mounted() {
    mapboxgl.accessToken = this.accessToken;

    var map = new mapboxgl.Map({
      container: "mapContainer",
      style: "mapbox://styles/mapbox/streets-v11",
      center: [-70.640698, -33.445043],
      zoom: 8,
    });
    // new mapboxgl.Marker()
    //   .setLngLat([-70.640698, -33.445043])
    //   .addTo(map);
    this.$nextTick(function () {
    
    var geojson = {
      'type': 'FeatureCollection',
      'features': [
      {
      'type': 'Feature',
      'properties': {
      'message': 'Baz',
      'iconSize': [25, 25]
      },
      'geometry': {
      'type': 'Point',
      'coordinates': [-70.640698, -33.445043]
      }
      }
      ]
    };

    // fin
    // add markers to map
    geojson.features.forEach(function (marker) {
      // Create a DOM element for each marker.
      var el = document.createElement('div');
      el.className = 'marker';
      el.style.backgroundColor = 'yellow';
      el.style.borderRadius = '50%';
      el.style.width = marker.properties.iconSize[0] + 'px';
      el.style.height = marker.properties.iconSize[1] + 'px';
      
      el.addEventListener('click', function () {
      window.alert(marker.properties.message);
    });
    
    // Add markers to the map.
    new mapboxgl.Marker(el)
    .setLngLat(marker.geometry.coordinates)
    .addTo(map);
    });

    
    
    // fin2
    })
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