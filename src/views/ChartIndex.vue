<template>
  <div class="pa-2">
    <div>
      <CandleIndex :volume-data="displayedObjects" :showEMA="showEMA5" />
    </div>

    <div class="my-3">
      <p class="mb-n14 ml-2">Volume</p>
      <volume-chart :volume-data="displayedObjects" />
    </div>

    <div style="height: 190px">
      <p class="mb-n14 ml-2">RSI</p>
      <RSI1Chart :volume-data="displayedObjects" v-if="showRSI" />
    </div>
    <div
      style="border: 1px solid red"
      :class="
        $vuetify.display.mdAndUp
          ? 'd-flex justify-space-around align-center py-7'
          : 'py-7'
      "
    >
      <div>
        <div>
          <v-checkbox
            v-model="showEMA5"
            label="EMA"
            color="green-darken-3"
            hide-details
          ></v-checkbox>
        </div>
        <div>
          <v-checkbox
            v-model="showRSI"
            label="RSI"
            color="red-darken-3"
            hide-details
          ></v-checkbox>
        </div>
      </div>
      <div class="pl-2">
        <div v-if="currentPage === 1">
          <v-btn color="blue-darken-2" @click="currentPage++">Next</v-btn>
        </div>
        <div v-else-if="currentPage === 2">
          <v-btn class="mt-2" color="red-darken-2" @click="currentPage--">
            Previous
          </v-btn>
        </div>
        <div v-if="currentPage === 2 && !showAll">
          <v-btn color="green-darken-2 mr-4 mt-2" @click="showMoreObjects">
            Click to Add
          </v-btn>
        </div>
        <div v-if="currentPage === 2 && !showAll">
          <v-btn
            color="red-darken-2"
            class="mt-2"
            v-if="currentPage === 2 && !showAll"
            @click="showAllObjects"
          >
            Show Automatically
          </v-btn>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import VolumeChart from "./VolumeChart.vue";
import CandleIndex from "./CandleIndex.vue";
import RSI1Chart from "./RSI1.vue";
export default {
  components: {
    VolumeChart,
    CandleIndex,
    RSI1Chart,
  },
  data: function () {
    return {
      showRSI: true,
      currentPage: 1,
      showAll: false,
      currentIndex: 20,

      showEMA5: false,
      data1: [
        {
          Date: 1675036800000,
          Open: 35.0,
          High: 36.25,
          Low: 35.0,
          Close: 36.0,
          Volume: 4022100,
          EMA50: 36.45,
          CMPR: 120.0,
        },
        {
          Date: 1675123200000,
          Open: 36.0,
          High: 36.0,
          Low: 34.75,
          Close: 34.75,
          Volume: 2950000,
          EMA50: 36.38,
          CMPR: 97.0,
        },
        {
          Date: 1675209600000,
          Open: 34.75,
          High: 35.5,
          Low: 34.5,
          Close: 34.75,
          Volume: 2213900,
          EMA50: 36.32,
          CMPR: 70.0,
        },
        {
          Date: 1675296000000,
          Open: 34.75,
          High: 35.0,
          Low: 34.0,
          Close: 34.0,
          Volume: 1965700,
          EMA50: 36.23,
          CMPR: 82.0,
        },
        {
          Date: 1675382400000,
          Open: 34.0,
          High: 34.5,
          Low: 34.0,
          Close: 34.0,
          Volume: 1027500,
          EMA50: 36.14,
          CMPR: 42.0,
        },
        {
          Date: 1675641600000,
          Open: 34.0,
          High: 34.75,
          Low: 33.75,
          Close: 34.5,
          Volume: 1181600,
          EMA50: 36.08,
          CMPR: 49.0,
        },
        {
          Date: 1675728000000,
          Open: 34.75,
          High: 38.5,
          Low: 34.5,
          Close: 38.0,
          Volume: 11192000,
          EMA50: 36.15,
          CMPR: 599.0,
        },
        {
          Date: 1675814400000,
          Open: 37.75,
          High: 39.25,
          Low: 36.5,
          Close: 37.5,
          Volume: 5282900,
          EMA50: 36.2,
          CMPR: 150.0,
        },
        {
          Date: 1675900800000,
          Open: 37.25,
          High: 38.75,
          Low: 36.75,
          Close: 38.5,
          Volume: 3024300,
          EMA50: 36.29,
          CMPR: 73.0,
        },
        {
          Date: 1675987200000,
          Open: 38.25,
          High: 39.25,
          Low: 38.0,
          Close: 38.5,
          Volume: 2316500,
          EMA50: 36.38,
          CMPR: 53.0,
        },
        {
          Date: 1676246400000,
          Open: 38.25,
          High: 38.5,
          Low: 37.25,
          Close: 38.0,
          Volume: 1883200,
          EMA50: 36.44,
          CMPR: 41.0,
        },
        {
          Date: 1676332800000,
          Open: 38.0,
          High: 38.25,
          Low: 34.75,
          Close: 35.5,
          Volume: 4495500,
          EMA50: 36.41,
          CMPR: 95.0,
        },
        {
          Date: 1676419200000,
          Open: 35.5,
          High: 36.0,
          Low: 33.75,
          Close: 34.0,
          Volume: 3137100,
          EMA50: 36.31,
          CMPR: 92.0,
        },
        {
          Date: 1676505600000,
          Open: 34.5,
          High: 35.0,
          Low: 33.25,
          Close: 34.75,
          Volume: 1717100,
          EMA50: 36.25,
          CMPR: 58.0,
        },
        {
          Date: 1676592000000,
          Open: 34.75,
          High: 35.0,
          Low: 34.25,
          Close: 34.75,
          Volume: 1101500,
          EMA50: 36.19,
          CMPR: 41.0,
        },
        {
          Date: 1676851200000,
          Open: 34.75,
          High: 36.0,
          Low: 34.5,
          Close: 35.0,
          Volume: 1277400,
          EMA50: 36.15,
          CMPR: 52.0,
        },
        {
          Date: 1676937600000,
          Open: 35.25,
          High: 35.5,
          Low: 34.75,
          Close: 35.0,
          Volume: 892200,
          EMA50: 36.1,
          CMPR: 38.0,
        },
        {
          Date: 1677024000000,
          Open: 35.0,
          High: 36.0,
          Low: 34.75,
          Close: 35.75,
          Volume: 847100,
          EMA50: 36.09,
          CMPR: 52.0,
        },
        {
          Date: 1677110400000,
          Open: 36.0,
          High: 38.0,
          Low: 36.0,
          Close: 37.75,
          Volume: 2863100,
          EMA50: 36.15,
          CMPR: 245.0,
        },
        {
          Date: 1677196800000,
          Open: 37.75,
          High: 38.0,
          Low: 36.25,
          Close: 36.75,
          Volume: 2549900,
          EMA50: 36.18,
          CMPR: 183.0,
        },
        {
          Date: 1677456000000,
          Open: 37.0,
          High: 37.5,
          Low: 36.25,
          Close: 37.5,
          Volume: 1421000,
          EMA50: 36.23,
          CMPR: 84.0,
        },
        {
          Date: 1677542400000,
          Open: 37.0,
          High: 38.0,
          Low: 36.5,
          Close: 38.0,
          Volume: 1567100,
          EMA50: 36.3,
          CMPR: 91.0,
        },
        {
          Date: 1677628800000,
          Open: 40.0,
          High: 40.75,
          Low: 37.0,
          Close: 37.0,
          Volume: 8535200,
          EMA50: 36.32,
          CMPR: 461.0,
        },
        {
          Date: 1677715200000,
          Open: 37.25,
          High: 39.25,
          Low: 37.0,
          Close: 38.25,
          Volume: 4008700,
          EMA50: 36.4,
          CMPR: 118.0,
        },
        {
          Date: 1677801600000,
          Open: 38.25,
          High: 38.75,
          Low: 38.0,
          Close: 38.5,
          Volume: 2157500,
          EMA50: 36.48,
          CMPR: 60.0,
        },
        {
          Date: 1678147200000,
          Open: 38.75,
          High: 42.0,
          Low: 38.75,
          Close: 41.25,
          Volume: 8612400,
          EMA50: 36.67,
          CMPR: 243.0,
        },
        {
          Date: 1678233600000,
          Open: 40.75,
          High: 43.5,
          Low: 39.75,
          Close: 43.0,
          Volume: 9223100,
          EMA50: 36.92,
          CMPR: 185.0,
        },
        {
          Date: 1678320000000,
          Open: 43.0,
          High: 43.25,
          Low: 41.0,
          Close: 41.5,
          Volume: 4790600,
          EMA50: 37.1,
          CMPR: 74.0,
        },
        {
          Date: 1678406400000,
          Open: 41.25,
          High: 41.25,
          Low: 39.5,
          Close: 40.25,
          Volume: 5198100,
          EMA50: 37.22,
          CMPR: 90.0,
        },
        {
          Date: 1678665600000,
          Open: 40.0,
          High: 41.75,
          Low: 39.25,
          Close: 40.0,
          Volume: 4445100,
          EMA50: 37.33,
          CMPR: 74.0,
        },
        {
          Date: 1678752000000,
          Open: 40.0,
          High: 40.75,
          Low: 38.5,
          Close: 39.0,
          Volume: 3341000,
          EMA50: 37.4,
          CMPR: 52.0,
        },
        {
          Date: 1678838400000,
          Open: 39.75,
          High: 42.25,
          Low: 39.25,
          Close: 42.25,
          Volume: 4376000,
          EMA50: 37.59,
          CMPR: 81.0,
        },
        {
          Date: 1678924800000,
          Open: 41.5,
          High: 42.5,
          Low: 41.0,
          Close: 42.0,
          Volume: 2980700,
          EMA50: 37.76,
          CMPR: 67.0,
        },
        {
          Date: 1679011200000,
          Open: 42.75,
          High: 43.0,
          Low: 39.25,
          Close: 40.25,
          Volume: 5683400,
          EMA50: 37.86,
          CMPR: 140.0,
        },
        {
          Date: 1679270400000,
          Open: 40.5,
          High: 41.25,
          Low: 39.5,
          Close: 39.5,
          Volume: 2902300,
          EMA50: 37.92,
          CMPR: 70.0,
        },
        {
          Date: 1679356800000,
          Open: 39.5,
          High: 40.25,
          Low: 37.75,
          Close: 38.5,
          Volume: 4812700,
          EMA50: 37.94,
          CMPR: 125.0,
        },
        {
          Date: 1679443200000,
          Open: 39.0,
          High: 39.5,
          Low: 37.75,
          Close: 38.25,
          Volume: 2022800,
          EMA50: 37.96,
          CMPR: 49.0,
        },
        {
          Date: 1679529600000,
          Open: 38.5,
          High: 40.25,
          Low: 38.5,
          Close: 40.0,
          Volume: 2386100,
          EMA50: 38.04,
          CMPR: 65.0,
        },
        {
          Date: 1679616000000,
          Open: 40.0,
          High: 40.0,
          Low: 39.0,
          Close: 39.25,
          Volume: 1129300,
          EMA50: 38.08,
          CMPR: 32.0,
        },
        {
          Date: 1679875200000,
          Open: 39.5,
          High: 40.5,
          Low: 38.75,
          Close: 40.25,
          Volume: 2855700,
          EMA50: 38.17,
          CMPR: 108.0,
        },
        {
          Date: 1679961600000,
          Open: 40.5,
          High: 40.5,
          Low: 39.75,
          Close: 40.25,
          Volume: 966200,
          EMA50: 38.25,
          CMPR: 37.0,
        },
        {
          Date: 1680048000000,
          Open: 40.5,
          High: 41.5,
          Low: 40.25,
          Close: 41.0,
          Volume: 2398900,
          EMA50: 38.36,
          CMPR: 128.0,
        },
        {
          Date: 1680134400000,
          Open: 41.0,
          High: 41.0,
          Low: 39.75,
          Close: 39.75,
          Volume: 1500400,
          EMA50: 38.41,
          CMPR: 77.0,
        },
        {
          Date: 1680220800000,
          Open: 40.0,
          High: 41.0,
          Low: 39.5,
          Close: 41.0,
          Volume: 1936000,
          EMA50: 38.51,
          CMPR: 109.0,
        },
        {
          Date: 1680480000000,
          Open: 41.25,
          High: 42.5,
          Low: 40.5,
          Close: 41.0,
          Volume: 4444800,
          EMA50: 38.61,
          CMPR: 230.0,
        },
        {
          Date: 1680566400000,
          Open: 41.0,
          High: 41.25,
          Low: 39.75,
          Close: 40.25,
          Volume: 1624500,
          EMA50: 38.68,
          CMPR: 72.0,
        },
        {
          Date: 1680652800000,
          Open: 40.25,
          High: 41.5,
          Low: 39.25,
          Close: 39.5,
          Volume: 2802800,
          EMA50: 38.71,
          CMPR: 118.0,
        },
        {
          Date: 1680825600000,
          Open: 39.75,
          High: 40.0,
          Low: 39.25,
          Close: 39.5,
          Volume: 720900,
          EMA50: 38.74,
          CMPR: 29.0,
        },
        {
          Date: 1681084800000,
          Open: 39.75,
          High: 41.75,
          Low: 38.75,
          Close: 41.0,
          Volume: 3116600,
          EMA50: 38.83,
          CMPR: 135.0,
        },
        {
          Date: 1681171200000,
          Open: 40.75,
          High: 42.25,
          Low: 40.5,
          Close: 41.5,
          Volume: 3255300,
          EMA50: 38.93,
          CMPR: 128.0,
        },
        {
          Date: 1681257600000,
          Open: 41.75,
          High: 45.25,
          Low: 40.5,
          Close: 44.25,
          Volume: 6756800,
          EMA50: 39.14,
          CMPR: 293.0,
        },
      ],
      visibleObjects: [],
    };
  },
  computed: {
    displayedObjects() {
      if (this.currentPage === 1) {
        return this.data1.slice(0, 20);
      } else if (this.currentPage === 2) {
        if (this.showAll) {
          return this.data1;
        } else {
          return this.visibleObjects;
        }
      }
      return 0;
    },
  },

  methods: {
    showMoreObjects() {
      // this.visibleObjects = this.data1.slice(0, 20);
      for (let i = this.currentIndex; i < this.currentIndex + 1; i++) {
        if (i < this.data1.length) {
          this.visibleObjects.push(this.data1[i]);
        }
      }
      this.currentIndex += 1;
    },
    // showAllObjects() {
    //   const remainingObjects = this.data1.slice(20);
    //   console.log(remainingObjects);
    //   let i = 0;
    //   const pushObject = () => {
    //     if (i < remainingObjects.length) {
    //       this.visibleObjects.push(remainingObjects[i]);
    //       i++;
    //       if (i === remainingObjects.length) {
    //         this.showAll = true;
    //       } else {
    //         // Recursively call this function to push the next object
    //         // after a small delay (to allow the UI to update)
    //         requestAnimationFrame(() => pushObject());
    //       }
    //     }
    //   };
    //   pushObject();
    // },

    showAllObjects() {
      // this.visibleObjects = this.data1.slice(0, 20);
      const remainingObjects = this.data1.slice(20);
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
<style></style>
  
        
    

