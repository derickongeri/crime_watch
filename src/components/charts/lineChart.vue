<template>
  <div
    class="q-my-none q-mt-none"
    style="
      max-height: 35vh;
      border: 0px solid rgb(160, 160, 160);
      position: relative;
      left: 0%;
    "
  >
    <Line
      :data="data"
      :chart-options="chartOptions"
      :chart-id="chartId"
      :dataset-id-key="datasetIdKey"
      :plugins="plugins"
      :css-classes="cssClasses"
      :styles="styles"
      :width="width"
      :height="height"
    />
  </div>
</template>

<script>
import { Line } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  PointElement,
  CategoryScale,
  Plugin,
} from "chart.js";

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  PointElement,
  CategoryScale
);

export default {
  name: "LineChart",
  components: { Line },
  props: {
    data: {
      type: Object,
      default: {
        labels: ["2015", "2016", "2017", "2018", "2019", "2020"],
        datasets: [
          {
            backgroundColor: "#b3cde0",
            borderColor: "#b3cde0",
            data: [30, 15, 18, 23, 29, 35],
            label: "Degraded",
            tension: 0.4
          },
          {
            backgroundColor: "#6497b1",
            borderColor: "#6497b1",
            data: [50, 70, 61, 57, 41, 45],
            label: "Stable",
            tension: 0.4
          },
          {
            backgroundColor: "#b3cde0",
            borderColor: "#b3cde0",
            data: [20, 15, 21, 20, 30, 20],
            label: "Improved",
            tension: 0.4
          },
        ],
      },
    },
    chartId: {
      type: String,
      default: "line-chart",
    },
    datasetIdKey: {
      type: String,
      default: "label",
    },
    width: {
      type: Number,
      default: 0,
    },
    height: {
      type: Number,
      default: 0,
    },
    cssClasses: {
      default: "",
      type: String,
    },
    styles: {
      type: Object,
      default: () => {},
    },
    plugins: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      chartOptions: {
        responsive: false,
        maintainAspectRatio: false,
        LineElement: {
          tension: 20,
        },
        scales: {
          x: {
            stacked: false,
            ticks: {
              color: "",
            },
            grid: {
              color: "",
              opacity: 0.4,
              borderDash: [5, 2],
              drawBorder: true,
            },
          },
          y: {
            stacked: false,
            ticks: {
              callback: function (value) {
                value = value.toFixed();
                return `${value}`;
              },
              color: "",
              tickLength: 0,
              tickWidth: 0,
            },
            grid: {
              color: "#9e9d24",
              opacity: 0.4,
              borderDash: [1, 10],
              drawBorder: false,
              tickLength: 0,
              tickWidth: 0,
            },
          },
        },
        plugins: {
          datalabels: {
            display: false,
          },
          legend: {
            display: false,
            position: "bottom",
            labels: {
              font: {
                fontColor: "#EEEEEE",
              },
              usePointStyle: true,
              pointStyle: "line",
              padding: 25,
            },
          },
          title: {
            display: false,
            text: "Crop Area in Ha",
            position: "top",
            align: "start",
            color: "#EEEEEE",
          },
        },
      },
    };
  },
};
</script>
