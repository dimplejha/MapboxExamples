<template>
  <head>
    <link
      href="https://api.mapbox.com/mapbox-gl-js/v2.10.0/mapbox-gl.css"
      rel="stylesheet"
    />
  </head>
  <v-map class="w-full h-full" :options="state.map" @loaded="onMapLoaded" />
</template>




<script setup lang="ts">
import VMap from "v-mapbox";
import mapboxgl from "mapbox-gl";
import MapboxGeocoder from "@mapbox/mapbox-gl-geocoder";

const state = reactive({
  map: {
    accessToken:
      "pk.eyJ1Ijoic29jaWFsZXhwbG9yZXIiLCJhIjoiREFQbXBISSJ9.dwFTwfSaWsHvktHrRtpydQ",
    style: "mapbox://styles/mapbox/streets-v11?optimize=true",
    center: [444.04931277036667, 26.266912177018096] as number[], //uses longitude, latitude
    zoom: 6,
    maxZoom: 22,
  },
});

function onMapLoaded(map: mapboxgl.Map) {
  console.log(state.map);

  // Create a default Marker and add it to the map.
  const marker1 = new mapboxgl.Marker()
    .setLngLat([12.554729, 55.70651])
    .addTo(map);

  // Create a default Marker, colored black, rotated 45 degrees.
  const marker2 = new mapboxgl.Marker({ color: "black", rotation: 45 })
    .setLngLat([12.65147, 55.608166])
    .addTo(map);
  //   map.on("load", () => {
  //     map.setFog({}); // Set the default atmosphere style
  //   });
}
</script>


<style >
#map {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}
</style>