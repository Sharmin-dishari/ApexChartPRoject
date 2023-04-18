<template>
  <div>
    <apexchart
      height="90"
      type="line"
      :options="options"
      :series="series"
      style="border: 1px solid grey"
    />
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
  methods: {
    formattedDate(timestamp) {
      const date = new Date(timestamp);
      const year = date.getFullYear();
      const month = (date.getMonth() + 1).toString().padStart(2, "0");
      const day = date.getDate().toString().padStart(2, "0");
      return `${year}-${month}-${day}`;
    },
  },
  computed: {
    options() {
      return {
        chart: {
          height: 150,
          type: "line",
          toolbar: {
            show: false,
          },
        },
        xaxis: {
          type: "datetime",
          categories: this.volumeData.map((data) => data.Date),
          labels: {
            show: false,
          },
        },
        yaxis: {
          labels: {
            show: false,
          },
        },
        series: [
          {
            name: "RSI",
            data: this.volumeData.map((item) => item.CMPR),
          },
        ],
        colors: ["#272323"],
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
