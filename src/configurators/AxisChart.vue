<template>
  <div>
    <div class="flex flex-wrap -mx-3 mb-4">
      <Data label="Title" placeholder="Your Awesome Title" v-model="chartConfig.title" width="two-third"/>
      <Data label="Height" placeholder="300" v-model="chartConfig.height" width="third"/>
    </div>
    <div class="flex flex-wrap -mx-3 mb-4">
      <Data
        label="Y-Marker Label"
        placeholder="Marker"
        v-model="chartConfig.data.yMarkers[0].label"
        width="half"
      />
      <Data
        label="Y-Marker Value"
        placeholder="70"
        type="number"
        v-model="chartConfig.data.yMarkers[0].value"
        width="half"
      />
    </div>
    <div class="flex flex-wrap -mx-3 mb-4">
      <Data label="Label" placeholder="Region" v-model="chartConfig.data.yRegions[0].label" width="third" />
      <Data label="Start" placeholder="-10" type="number" v-model="chartConfig.data.yRegions[0].start" width="third" />
      <Data label="End" placeholder="50" type="number" v-model="chartConfig.data.yRegions[0].end" width="third" />
    </div>
  </div>
</template>
<script>
import Data from "@/controls/Data";

export default {
  name: "AxisChart",
  components: {
    Data: Data
  },
  data() {
    return {
      chartConfig: {
        title: "My Awesome Chart",
        type: "axis-mixed", // or 'bar', 'line', 'scatter', 'pie', 'percentage'
        height: 350,
        truncateLegends: 1,
        data: {
          labels: [
            "12am-3am",
            "3am-6am",
            "6am-9am",
            "9am-12pm",
            "12pm-3pm",
            "3pm-6pm",
            "6pm-9pm",
            "9pm-12am"
          ],
          datasets: [
            {
              name: "Some Data",
              chartType: "bar",
              values: [25, 40, 30, 35, 8, 52, 17, -4]
            },
            {
              name: "Another Set",
              chartType: "bar",
              values: [25, 50, -10, 15, 18, 32, 27, 14]
            },
            {
              name: "Yet Another Label",
              chartType: "line",
              values: [15, 20, -3, -15, 58, 12, -17, 37]
            }
          ],
          yMarkers: [
            { label: "Marker", value: 70, options: { labelPos: "left" } }
          ],
          yRegions: [
            {
              label: "Region",
              start: -10,
              end: 50,
              options: { labelPos: "right" }
            }
          ]
        },
      }
    };
  },
  mounted() {
    this.$emit('updateChart', this.chartConfig);
  },
  watch: {
    chartConfig: {
      handler: function () {
        this.$emit('updateChart', this.chartConfig);
      },
      deep: true
    }
  }
};
</script>