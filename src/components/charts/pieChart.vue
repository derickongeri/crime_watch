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
    <Pie
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
import { Pie } from "vue-chartjs";
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  ArcElement,
  CategoryScale,
  Plugin,
} from "chart.js";
// import ChartDataLabels from "chartjs-plugin-datalabels";

ChartJS.register(
  Title,
  Tooltip,
  Legend,
  ArcElement,
  CategoryScale,
);

export default {
  name: "BarChart",
  components: { Pie },
  props: {
    chartOptions: {
      type: Object,
      default: {
        responsive: true,
        maintainAspectRatio: false,
        plugins: {
          // datalabels: {
          //   display: "auto",
          //   anchor: "center",
          //   align: "center",
          //   offset: 4,
          //   opacity: 0.7,
          //   formatter: (val, ctx) => {
          //     // Grab the label for this value
          //     const label = ctx.chart.data.labels[ctx.dataIndex];

          //     // Format the number with 2 decimal places
          //     const formattedVal = Intl.NumberFormat("en-US", {
          //       minimumFractionDigits: 1,
          //     }).format(val);

          //     // Put them together
          //     return `${formattedVal} %`;
          //   },
          //   borderRadius: 5,
          //   leftborderWidth: 2,
          //   borderColor: ["#b71c1c", "#2e7d32", "#fff9b4"],
          //   color: "#404040",
          //   size: "8",
          //   backgroundColor: "#fff",
          // },
          legend: {
            display: false,
            position: "left",
            labels: {
              font: {
                fontColor: "#EEEEEE",
              },
              usePointStyle: true,
              padding: 25,
            },
          },
          title: {
            display: false,
            align: "start",
            text: "Crop Area in Ha",
            position: "top",
            color: "#404040",
          },
        },
      },
    },
    data: {
      type: Object,
      default: {
        labels: ["Degraded", "new", "Improved", "Stable"],
        datasets: [
          {
            backgroundColor: ["#b3cde0", "#6497b1", "#b3cde0"],
            borderColor: "rgba(0, 0, 0, 0)",
            borderRadius: 0,
            borderWidth: 0,
            spacing: 0,
            cutout: "75",
            radius: "80%",
            data: [20, 30, 50],
          },
        ],
      },
      required: true,
    },
    chartId: {
      type: String,
      default: "pie-chart",
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
      // chartOptions: {
      //   responsive: true,
      //   plugins: {
      //     legend: {
      //       display: true,
      //       position: "right",
      //       labels: {
      //         font: {
      //           fontColor: "#EEEEEE",
      //         },
      //       },
      //     },
      //     title: {
      //       display: false,
      //       text: "Crop Area in Ha",
      //       position: "left",
      //       color: "#EEEEEE",
      //     },
      //   },
      // },
    };
  },
};
</script>
