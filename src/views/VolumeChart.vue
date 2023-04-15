<template>
  <div>
    <apexchart type="bar" :options="chartOptions" :series="series"></apexchart>
  </div>
</template>

<script>
import VueApexCharts from "vue3-apexcharts";

export default {
  name: "ColumnChart",
  components: {
    apexchart: VueApexCharts,
  },
  data() {
    return {
      series: [
        {
          data: [30, 40, 45, 50, 49, 60, 70, 91, 125],
        },
      ],
      chartOptions: {
        chart: {
          type: "bar",
          height: 350,
          toolbar: {
            show: false,
          },
        },
        plotOptions: {
          bar: {
            columnWidth: "45%",
            distributed: true,
          },
        },
        dataLabels: {
          enabled: false,
        },
        xaxis: {
          categories: [
            "Jan",
            "Feb",
            "Mar",
            "Apr",
            "May",
            "Jun",
            "Jul",
            "Aug",
            "Sep",
          ],
          labels: {
            style: {
              fontSize: "14px",
            },
          },
        },
        yaxis: {
          title: {
            text: "Sales",
            style: {
              fontSize: "14px",
            },
          },
          labels: {
            style: {
              fontSize: "14px",
            },
          },
        },
        tooltip: {
          enabled: true,
          style: {
            fontSize: "14px",
          },
        },
      },
    };
  },
};
</script>
