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
import MapboxDraw from "@mapbox/mapbox-gl-draw";

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
  map.addSource("maine", {
    type: "geojson",
    data: {
      type: "FeatureCollection",
      features: [
        {
          type: "Feature",
          properties: {},
          geometry: {
            type: "Polygon",
            coordinates: [
              [
                [-15.468749999999998, 7.710991655433217],
                [-4.5703125, -21.289374355860424],
                [33.046875, -11.867350911459294],
                [12.65625, 7.710991655433217],
                [-15.468749999999998, 7.710991655433217],
              ],
            ],
          },
        },
      ],
    },
  });
  // Add a new layer to visualize the polygon.
  map.addLayer({
    id: "maine",
    type: "fill",
    source: "maine", // reference the data source
    layout: {},
    paint: {
      "fill-color": "#0080FF", // blue color fill
      "fill-opacity": 0.5,
    },
  });
  // Add a black outline around the polygon.
  map.addLayer({
    id: "outline",
    type: "line",
    source: "maine",
    layout: {},
    paint: {
      "line-color": "#000",
      "line-width": 3,
    },
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




