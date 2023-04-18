<template>
  <div>
    <apexchart type="line" :options="chartOptions" :series="seriesData" />
    <div class="text-center">
      <v-btn v-if="currentPage === 1" @click="currentPage++">Next</v-btn>
      <v-btn
        class="mx-md px=md"
        v-else-if="currentPage === 2"
        @click="currentPage--"
      >
        Previous
      </v-btn>
      <v-btn v-if="currentPage === 2" @click="showAllObjects"> Show All </v-btn>
    </div>
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
    return {
      currentPage: 1,
      showAll: false,
      visibleObjects: [],

      chartOptions: {
        height: 350,
        type: "line",
      },
      stroke: {
        width: [3, 1],
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
      xaxis: {
        type: "datetime",
      },
      yaxis: {
        tooltip: {
          enabled: true,
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
    displayedObjects() {
      if (this.currentPage === 1) {
        return this.volumeData.slice(0, 20);
      } else if (this.currentPage === 2) {
        if (this.showAll) {
          return this.volumeData;
        } else {
          return this.visibleObjects;
        }
      }
      return 0;
    },
    seriesData() {
      return [
        {
          name: "EMA",
          type: "line",
          data: this.displayedObjects.map((obj) => ({
            x: this.formattedDate(obj.Date),
            y: obj.EMA50,
          })),
        },
        {
          name: "CANDLE",
          type: "candlestick",
          data: this.displayedObjects.map((obj) => ({
            x: this.formattedDate(obj.Date),
            y: [obj.Open, obj.High, obj.Low, obj.Close],
          })),
        },
      ];
    },
  },
  methods: {
    showAllObjects() {
      const remainingObjects = this.volumeData.slice(20);
      console.log(remainingObjects, "remaining");
      let i = 0;
      const interval = setInterval(() => {
        if (i < remainingObjects.length) {
          this.visibleObjects.push(remainingObjects[i]);
          i++;
        } else {
          clearInterval(interval);
          this.showAll = true;
        }
      }, 1000);
      this.showAll = false; // Change the interval time to adjust the speed of showing objects
    },
    formattedDate(timestamp) {
      const date = new Date(timestamp);
      const year = date.getFullYear();
      const month = (date.getMonth() + 1).toString().padStart(2, "0");
      const day = date.getDate().toString().padStart(2, "0");
      return `${year}-${month}-${day}`;
    },
  },
};
</script>
