<template>
  <div>
    <apexchart type="line" :options="options" :series="series" />
  </div>
</template>

<script>
import VueApexCharts from "vue3-apexcharts";

export default {
  components: {
    apexchart: VueApexCharts,
  },
  props: {
    volumeData: Array,
  },
  data() {
    return {};
  },
  computed: {
    options() {
      return {
        chart: {
          height: 350,
          type: "line",
          toolbar: {
            show: false,
          },
        },
        xaxis: {
          categories: this.volumeData.map((data) => data.Date),
        },
        yaxis: {
          opposite: true,
        },
        series: [
          {
            name: "RSI",
            data: this.volumeData.map((item) => item.CMPR),
          },
        ],
        colors: ["#FF4560"],
        stroke: {
          width: 2,
        },
        tooltip: {
          shared: true,
          intersect: false,
        },
        grid: {
          padding: {
            right: 20,
          },
        },
      };
    },

    series() {
      return [
        {
          name: "RSI",
          data: this.volumeData.map((item) => item.EMA50),
        },
      ];
    },
  },
};
</script>
