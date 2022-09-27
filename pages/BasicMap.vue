<template>
  <head>
    <link
      href="https://api.mapbox.com/mapbox-gl-js/v2.10.0/mapbox-gl.css"
      rel="stylesheet"
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
</script>



<style >
#map {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}
</style>




