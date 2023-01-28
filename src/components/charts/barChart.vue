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
  <Bar
    :data="data"
    :options="options"
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
import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  BarElement,
  CategoryScale,
  LinearScale,
} from "chart.js";
import { Bar } from "vue-chartjs";

ChartJS.register(
  CategoryScale,
  LinearScale,
  BarElement,
  Title,
  Tooltip,
  Legend
);

export default {
  name: "App",
  components: {
    Bar,
  },
  props: {
    data: {
      type: Object,
      default: {
        labels: [
          "January",
          "February",
          "March",
          "April",
          "May",
          "June",
          "July",
          "August",
          "September",
          "October",
          "November",
          "December",
        ],
        datasets: [
          {
            label: "Data One",
            backgroundColor: "#b3cde0",
            data: [40, 20, 12, 39, 10, 40, 39, 80, 40, 20, 12, 11],
          },
        ],
      },
    },
    chartId: {
      type: String,
      default: "bar-chart",
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
        layout: {
          padding: 0,
        },
        responsive: false,
        maintainAspectRatio: false,
        plugins: {
          datalabels: {
            display: "auto",
            anchor: "end",
            align: "end",
            offset: 10,
            opacity: 0.9,
            formatter: (val, ctx) => {
              // Grab the label for this value
              const label = ctx.chart.data.labels[ctx.dataIndex];

              // Format the number with 2 decimal places
              const formattedVal = Intl.NumberFormat("en-US", {
                minimumFractionDigits: 1,
              }).format(val);

              // Put them together
              return `${formattedVal} %`;
            },
            borderRadius: 5,
            leftborderWidth: 2,
            borderColor: ["#b71c1c", "#2e7d32", "#fff9b4"],
            color: "#404040",
            size: "11",
            backgroundColor: "#fff",
          },
          legend: {
            display: false,
            position: "bottom",
            labels: {
              font: {
                fontColor: "#EEEEEE",
              },
            },
          },
          title: {
            display: true,
            text: "Land Area",
            position: "bottom",
            color: "#9e9d24",
          },
        },
        indexAxis: "y",
        elements: {
          bar: {
            borderWidth: 0,
            inflateAmount: 0,
            borderRadius: 20,
            borderSkipped: false,
          },
        },
        scales: {
          x: {
            min: 0,
            max: 100,
            ticks: {
              callback: function (value) {
                value = value.toFixed();
                return `${value}`;
              },
              color: "",
            },
            grid: {
              color: "",
            },
          },
          y: {
            ticks: {
              color: "",
              tickLength: 0,
            },
            grid: {
              color: "#9e9d24",
              borderDash: [1, 10],
              drawBorder: false,
              tickLength: 0,
              tickWidth: 0,
            },
          },
        },
      },
    };
  },
};
</script>
