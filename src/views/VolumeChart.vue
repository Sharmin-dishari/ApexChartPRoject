<template>
  <div>
    <apexchart height="150" type="bar" :options="chartOptions" :series="series" style="border: 1px solid grey"></apexchart>
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
          height: 150,
           toolbar: {
            show: false,
          },

          
        },
        plotOptions: {
          bar: {
            columnWidth: '80%',
            colors: {
              ranges: [
                {
                  from: 0,
                  to: 3000000,
                  color: "#f44336",
                },
                {
                  from: 3000000,
                  to: 100000000,
                  color: "#1ba44f",
                },
]

            },
          }
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
          opposite: true,
          labels: {
            formatter: function (value) {
              return value / 1000000 + "M";
            },
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
