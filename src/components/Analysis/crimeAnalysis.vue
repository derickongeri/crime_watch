<template>
  <div class="chartarea q-pa-md">
    <q-card flat class="chart-card" style="position:relative; max-height:90%; background: none;">
      <q-card-section>
        <barChart />
      </q-card-section>
      <q-card-section>
        <lineChart />
      </q-card-section>
      <q-card-section>
        <pieChart />
      </q-card-section>
    </q-card>
  </div>
</template>

<script>
import { ref } from "vue"
import setChartMethods from "src/composables/chartMethods.js";

export default {
  components: {
    barChart: require("components/charts/barChart.vue").default,
    lineChart: require("components/charts/lineChart.vue").default,
    pieChart: require("components/charts/pieChart.vue").default,
  },

};
</script>

<style>
.chartarea{
  position: relative;
  max-height: 90%;
  overflow: hidden;
}
</style>
