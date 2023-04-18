<template>
  <div>
    <apexchart height="500" type="line"  :options="chartOptions" :series="seriesFilteredData" style="border: 1px solid grey"/>
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
    showEMA: { type: Boolean, default: false }
  },
  data() {
    return {
      chartOptions: {
        chart: {
          type: "bar",
          height: 350,
          toolbar: {
            show: false,
          },

        },
      stroke: {
        width: [2, 1],
      },
      tooltip: {
        shared: true,
        custom: [
          function ({ seriesIndex, dataPointIndex, w }) {
            return w.globals.series[seriesIndex][dataPointIndex];
          },
          function ({ seriesIndex, dataPointIndex, w }) {
            var o = w.globals.seriesCandleO[seriesIndex][dataPointIndex];
            var h = w.globals.seriesCandleH[seriesIndex][dataPointIndex];
            var l = w.globals.seriesCandleL[seriesIndex][dataPointIndex];
            var c = w.globals.seriesCandleC[seriesIndex][dataPointIndex];
            return "";
          },
        ],
      },
        dataLabels: {
          enabled: false
        },
        colors: ["#272323"],
        legend: {
          show: false
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
        tooltip: {
          enabled: true,
        },
      },
 },
    };
  },
  computed: {
    // displayedObjects() {
    //   const start = (this.currentPage - 1) * 20;
    //   const end = start + 20;
    //   return this.volumeData.slice(start, end);
    // },
    seriesData() {
      return [
        {
          name: "EMA",
          type: "line",
          data: this.volumeData.map((obj) => ({
            x: this.formattedDate(obj.Date),
            y: obj.EMA50,
          })),
        },
        {
          name: "CANDLE",
          type: "candlestick",
          data: this.volumeData.map((obj) => ({
            x: this.formattedDate(obj.Date),
            y: [obj.Open, obj.High, obj.Low, obj.Close],
          })),
        },
      ];
    },
    seriesFilteredData () {
    if (!this.showEMA) {
    return [
         {
            name: "CANDLE",
            type: "candlestick",
            data: this.volumeData.map((obj) => ({
              x: this.formattedDate(obj.Date),
              y: [obj.Open, obj.High, obj.Low, obj.Close],
            })),
          }]}
          else{
           return [
          {
            name: "EMA",
            type: "line",
            data: this.volumeData.map((obj) => ({
              x: this.formattedDate(obj.Date),
              y: obj.EMA50,
            })),
          },
          {
            name: "CANDLE",
            type: "candlestick",
            data: this.volumeData.map((obj) => ({
              x: this.formattedDate(obj.Date),
              y: [obj.Open, obj.High, obj.Low, obj.Close],
            })),
          },
        ]   
    }
    },
  },
    methods: {
    formattedDate(timestamp) {
        const date = new Date(timestamp);
        const year = date.getFullYear();
        const month = (date.getMonth() + 1).toString().padStart(2, "0");
        const day = date.getDate().toString().padStart(2, "0");
        return `${year}-${month}-${day}`;
      },
    }
  }
</script>
