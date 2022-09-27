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
    center: [73.85696411132812, 18.536908560288477], // starting position
    zoom: 10,
    maxZoom: 55,
  },
});

function onMapLoaded(map) {
  map.on("load", () => {
    map.addSource("mapbox-terrain", {
      type: "vector",
      // Use any Mapbox-hosted tileset using its tileset id.
      // Learn more about where to find a tileset id:
      // https://docs.mapbox.com/help/glossary/tileset-id/
      url: "mapbox://mapbox.mapbox-terrain-v2",
    });
    map.addLayer({
      id: "terrain-data",
      type: "line",
      source: "mapbox-terrain",
      "source-layer": "contour",
      layout: {
        "line-join": "round",
        "line-cap": "round",
      },
      paint: {
        "line-color": "#ff69b4",
        "line-width": 1,
      },
    });
  });
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




