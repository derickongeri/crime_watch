<template>
  <div id="mapid"></div>
</template>

<script>
import { defineComponent, onMounted, ref } from "vue";

import L from "leaflet";
import "leaflet/dist/leaflet.css";

import baselayers from "./Modals/baselayers.js";

export default defineComponent({
  setup() {
    const map = ref(null),
      center = ref([-1, 35]),
      baseMaps = ref([]);

    const setLeafletMap = function () {
      const { osmTiles, darkMap, satellite } = baselayers;

      baseMaps.value = {
        OSM: osmTiles,
        satellite: satellite,
        darkMap: darkMap,
      };

      map.value = L.map("mapid", {
        zoomControl: false,
        layersControl: false,
        attributionControl: false,
        //maxBounds: bounds,
        minZoom: 3,
        maxZoom: 17,
      }).setView(center.value, 3);

      L.tileLayer(
        "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}{r}?access_token={accessToken}",
        {
          attribution:
            'Map data (c) <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery (c) <a href="https://www.mapbox.com/">Mapbox</a>',

          id: "mapbox/satellite-v9",
          accessToken:
            "pk.eyJ1IjoiY2hyaXNiYXJ0IiwiYSI6ImNrZTFtb3Z2bDAweTMyem1zcmthMGY0ejQifQ.3PzoCgSiG-1-sV1qJvO9Og",
        }
      ).addTo(map.value);

      L.control.layers(baseMaps.value).addTo(map.value);
    };

    onMounted(() => {
      setLeafletMap();
    });

    return {
      map,
    };
  },
});
</script>

<style scoped>
#mapid {
  position: absolute;
  top: 0;
  width: 60%;
  height: 60%;
  bottom: 0;
  box-shadow: inset 0px 0px 56vw 16vw rgba(0, 0, 0, 0.5);
  border-radius: 20px;
  margin: 10px;
}
</style>
