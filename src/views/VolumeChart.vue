<template>
  <div>
    <apexchart type="bar" :options="chartOptions" :series="series"></apexchart>
  </div>
</template>

<script>
import VueApexCharts from "vue3-apexcharts";

export default {
  name: "VolumeChart",
  components: {
    apexchart: VueApexCharts,
  },
  props: {
    volumeData: Array,
  },
  computed: {
    chartOptions() {
      return {
        chart: {
          type: "bar",
          height: 350,
        },
        plotOptions: {
          bar: {
            horizontal: false,
            columnWidth: "80%",
            colors: {
              ranges: [
                {
                  from: 0,
                  to: 1000000,
                  color: "#FFB64D",
                },
                {
                  from: 1000000,
                  to: 5000000,
                  color: "#FF4D4D",
                },
                {
                  from: 5000000,
                  to: 10000000,
                  color: "#6E4C41",
                },
                {
                  from: 10000000,
                  to: 20000000,
                  color: "#9932CC",
                },
                {
                  from: 20000000,
                  to: 50000000,
                  color: "#008000",
                },
                {
                  from: 50000000,
                  to: 100000000,
                  color: "#00FFFF",
                },
                {
                  from: 100000000,
                  to: 500000000,
                  color: "#1E90FF",
                },
                {
                  from: 500000000,
                  to: 1000000000,
                  color: "#9400D3",
                },
              ],
              gradient: {
                shade: "light",
                type: "horizontal",
                shadeIntensity: 0.25,
                gradientToColors: undefined,
                inverseColors: true,
                opacityFrom: 0.85,
                opacityTo: 0.85,
                stops: [0, 50, 100],
                colorStops: [],
              },
            },
          },
        },
        dataLabels: {
          enabled: false,
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
            formatter: function (value) {
              return value / 1000000 + "M";
            },
          },
        },
        title: {
          text: "Volume Chart",
          align: "center",
          style: {
            fontSize: "20px",
            fontWeight: "bold",
            fontFamily: undefined,
            color: "#263238",
          },
        },
      };
    },
    series() {
      return [
        {
          name: "Volume",
          data: this.volumeData.map((data) => data.Volume),
        },
      ];
    },
  },
};
</script>
