<template>
  <div>
    <div class="flex flex-wrap -mx-3 mb-4">
      <Data label="Title" placeholder="Your Awesome Title" v-model="chartConfig.title" width="two-third"/>
      <Data label="Height" placeholder="300" v-model="chartConfig.height" width="third"/>
    </div>
    <div class="flex flex-wrap -mx-3 mb-4">
      <Toggle label="Heatline" v-model="chartConfig.lineOptions.heatline" width="third"/>
      <Toggle label="Fill" v-model="chartConfig.lineOptions.regionFill" width="third"/>
      <Toggle label="Spline" v-model="chartConfig.lineOptions.spline" width="third"/>
    </div>
    <div class="flex flex-wrap -mx-3 mb-4">
      <Toggle label="Hide Dots" v-model="chartConfig.lineOptions.hideDots" width="third"/>
      <Toggle label="Hide Line" v-model="chartConfig.lineOptions.hideLine" width="third"/>
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
import Toggle from "@/controls/Toggle";
import { barCompositeData } from "@/data.js"

export default {
  name: "LineChart",
  components: {
    Data: Data,
    Toggle: Toggle
  },
  data() {
    return {
      chartConfig: {
        title: "My Awesome Chart",
        type: "line", // or 'bar', 'line', 'scatter', 'pie', 'percentage'
        height: 300,
        truncateLegends: 1,
        lineOptions: {
          heatline: 1,
          regionFill: 1,
          spline: 1,
          hideDots: 1,
          hideLine: 0,
        },
        data: {
          ...barCompositeData,
          yMarkers: [
            { label: "Marker", value: 70, options: { labelPos: "left" } }
          ],
          yRegions: [
            {
              label: "Region",
              start: 0,
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
        console.log(this.chartConfig);
        this.$emit('updateChart', this.chartConfig);
      },
      deep: true
    }
  }
};
</script>