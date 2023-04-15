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
  data() {
    return {
      options: {
        chart: {
          height: 350,
          type: "line",
          toolbar: {
            show: false,
          },
        },
        xaxis: {
          categories: [
            "01/01/2022",
            "02/01/2022",
            "03/01/2022",
            "04/01/2022",
            "05/01/2022",
            "06/01/2022",
            "07/01/2022",
            "08/01/2022",
            "09/01/2022",
            "10/01/2022",
          ],
        },
        yaxis: {
          opposite: true,
        },
        series: [
          {
            name: "RSI",
            data: [50, 60, 55, 45, 40, 35, 30, 35, 40, 50],
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
      },
      series: [
        {
          name: "RSI",
          data: [50, 60, 55, 45, 40, 35, 30, 35, 40, 50],
        },
      ],
    };
  },
};
</script>
