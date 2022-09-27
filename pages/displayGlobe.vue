<template>
  <head>
    <link
      href="https://api.mapbox.com/mapbox-gl-js/v2.10.0/mapbox-gl.css"
      rel="stylesheet"
    />
  </head>

  <v-map
    class="w-full h-full"
    :options="state.map"
    @loaded="onMapLoaded"
  ></v-map>

  <div id="map"></div>
</template>


<script setup lang="ts">
import VMap from "v-mapbox";
import mapboxgl from "mapbox-gl";

mapboxgl.accessToken =
  "pk.eyJ1Ijoic29jaWFsZXhwbG9yZXIiLCJhIjoiREFQbXBISSJ9.dwFTwfSaWsHvktHrRtpydQ";
//const data: string;
const state = reactive({
  map: {
    container: "map",
    style: "mapbox://styles/mapbox/satellite-streets-v11",
    center: [444.04931277036667, 26.266912177018096] as number[],
    zoom: 1.5,
    center: [30, 50],
    projection: "globe",
  },
});

function onMapLoaded(map: mapboxgl.Map) {
  map.on("load", () => {
    // Set the default atmosphere style
    map.setFog({});
  });
}
</script>



<style>
/* body {
  margin: 0;
  padding: 0;
} */
#map {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}
</style>
