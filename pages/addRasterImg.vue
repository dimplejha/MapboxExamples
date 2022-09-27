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
import sdk from "@mapbox/mapbox-sdk";
import MapboxGeocoder from "@mapbox/mapbox-gl-geocoder";

mapboxgl.accessToken =
  "pk.eyJ1Ijoic29jaWFsZXhwbG9yZXIiLCJhIjoiREFQbXBISSJ9.dwFTwfSaWsHvktHrRtpydQ";
const state = reactive({
  map: {
    container: "map",
    style: "mapbox://styles/mapbox/dark-v10", // style URL
    center: [11.255, 43.77], // starting position
    zoom: 1, // starting zoom
    maxZoom: 22,
  },
});

function onMapLoaded(map) {
  map.addControl(new mapboxgl.NavigationControl(), "top-left");

  map.on("load", () => {
    map.addSource("radar", {
      type: "image",
      url: "assets/images/downlode.jpg",
      coordinates: [
        [-80.425, 46.437],
        [-71.516, 46.437],
        [-71.516, 37.936],
        [-80.425, 37.936],
      ],
    });
    map.addLayer({
      id: "radar-layer",
      type: "raster",
      source: "radar",
      paint: {
        "raster-fade-duration": 0,
      },
    });
  });
}
</script>

<style>
#map {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
}
</style>
