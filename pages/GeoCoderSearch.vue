<template>
  <head>
    <link
      href="https://api.mapbox.com/mapbox-gl-js/v2.10.0/mapbox-gl.css"
      rel="stylesheet"
    />
    <link
      rel="stylesheet"
      href="https://api.mapbox.com/mapbox-gl-js/plugins/mapbox-gl-geocoder/v5.0.0/mapbox-gl-geocoder.css"
      type="text/css"
    />
  </head>
  <div id="map"></div>
  <v-map
    class="w-full h-full"
    :options="state.map"
    @loaded="onMapLoaded"
  ></v-map>
</template>

<script setup lang="ts">
import VMap from "v-mapbox";
import mapboxgl from "mapbox-gl";
import MapboxGeocoder from "@mapbox/mapbox-gl-geocoder";

mapboxgl.accessToken =
  "pk.eyJ1Ijoic29jaWFsZXhwbG9yZXIiLCJhIjoiREFQbXBISSJ9.dwFTwfSaWsHvktHrRtpydQ";
const state = reactive({
  map: {
    container: "map",
    style: "mapbox://styles/mapbox/outdoors-v11", // style URL
    center: [11.255, 43.77], // starting position
    zoom: 1, // starting zoom
    maxZoom: 22,
  },
});

function onMapLoaded(map: mapboxgl.Map) {
  const geocoder = new MapboxGeocoder({
    accessToken:
      "pk.eyJ1Ijoic29jaWFsZXhwbG9yZXIiLCJhIjoiREFQbXBISSJ9.dwFTwfSaWsHvktHrRtpydQ",
    marker: {
      color: "orange",
    },
    mapboxgl: mapboxgl,
  });

  map.addControl(geocoder);
}
</script>



<style >
#map {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}

#geocoder-container > div {
  min-width: 50%;
  margin-left: 25%;
}
</style>




