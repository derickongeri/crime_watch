<template>
  <div class="q-pa-xs" id="mapid"></div>
</template>

<script>
import { defineComponent, onMounted, ref } from "vue";
import { axios } from "src/boot/axios";

import L from "leaflet";
import "leaflet/dist/leaflet.css";

import baselayers from "./Modals/baselayers.js";
// import counties_2021 from './Modals/counties_2021.js'

export default defineComponent({
  setup() {
    const map = ref(null),
      center = ref([0, 37]),
      baseMaps = ref([]);

    const setLeafletMap = async function () {
      const { osmTiles, darkMap, satellite } = baselayers;

      // const counties = counties_2021

      baseMaps.value = {
        OSM: osmTiles,
        satellite: satellite,
        darkMap: darkMap,
      };

      const southWest = L.latLng(-4.702270507977403, 33.911819457602064),
        northEast = L.latLng(5.430648327058812, 41.906257629386246),
        bounds = L.latLngBounds(southWest, northEast);

      map.value = L.map("mapid", {
        zoomControl: false,
        layersControl: true,
        attributionControl: false,
        center: center.value,
        maxBounds: bounds,
        zoom: 6.3,
        maxZoom: 6.5,
        zoomSnap: 0.1,
        zoomAnimation: true,
        fadeAnimation: true,
        // layers: [darkMap, osm, mapbox, mapboxSatellite]
        //layers: [satellite],
      });

      // L.tileLayer(
      //   "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}{r}?access_token={accessToken}",
      //   {
      //     attribution:
      //       'Map data (c) <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',

      //     id: "mapbox/satellite-v9",
      //     accessToken:
      //       "pk.eyJ1IjoiY2hyaXNiYXJ0IiwiYSI6ImNrZTFtb3Z2bDAweTMyem1zcmthMGY0ejQifQ.3PzoCgSiG-1-sV1qJvO9Og",
      //   }
      // ).addTo(map.value);

      // L.control.layers(baseMaps.value).addTo(map.value);
    };

    const setVector = async function () {
      let wfsUrl =
        "http://78.141.234.158/geoserver/kenyadata/ows?service=WFS&version=1.0.0&request=GetFeature&typeName=kenyadata%3A2021_county&maxFeatures=250&outputFormat=application%2Fjson";

      let response = await axios.get(wfsUrl);

      const crimeIndexArray = response.data.features;
      let crimeIndexvalues = [];

      crimeIndexArray.forEach((d) => {
        crimeIndexvalues.push(d.properties.CRIME_INDE);
      });

      const maxVal = Math.max(...crimeIndexvalues);
      const minVal = Math.min(...crimeIndexvalues);

      const classInterval =
        (Math.max(...crimeIndexvalues) - Math.min(...crimeIndexvalues)) / 7;

      console.log(classInterval);

      console.log(crimeIndexvalues);

      function getColor(d) {
        return d > maxVal
          ? "#011f4b"
          : d > minVal + classInterval * 5
          ? "#03396c"
          : d > minVal + classInterval * 4
          ? "#005b96"
          : d > minVal + classInterval * 3
          ? "#6497b1"
          : d > minVal + classInterval * 2
          ? "#b3cde0"
          : d > minVal + classInterval * 1
          ? "#b3cde0"
          : d > minVal
          ? "#b3cde0"
          : "#b3cde0";
      }

      function style(feature) {
        return {
          fillColor: getColor(feature.properties.CRIME_INDE),
          weight: 2,
          opacity: 1,
          color: "white",
          dashArray: "3",
          fillOpacity: 0.7,
        };
      }

      const jsonLayer = L.geoJSON([response.data], { style: style });

      jsonLayer.addTo(map.value).bringToFront();
      map.value.fitBounds(jsonLayer.getBounds())
    };

    onMounted(() => {
      setLeafletMap();
      setVector();
    });

    return {
      map,
    };
  },
});
</script>

<style scoped>
#mapid {
  position: relative;
  top: 0%;
  left: 0%;
  width: 65%;
  height: 70vh;
  bottom: 0%;
  border-radius: 20px;
  background: none;
}
</style>
