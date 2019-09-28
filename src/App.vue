<template>
  <div class="flex">
    <div
      class="w-1/4 flex flex-col justify-between bg-white overflow-hidden md:h-screen min-h-full shadow-lg p-5"
    >
      <div class="chart-config">
        <Title/>
        <Options label="Chart Type" :options="chartTypes" width="full" v-model="chartType" @input="changeComponent"/>
        <component :is="currentComponent" @updateChart="updateChart"/>
      </div>
      <!-- <div id="controls">
        <div class="flex flex-row">
          <button
            class="bg-gray-500 hover:bg-gray-400 text-gray-200 font-semibold mt-5 mr-2 py-2 px-4 border-b-4 border-gray-700 hover:border-gray-500 rounded w-1/6"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 30 24"
              fill="none"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
              class="feather feather-download"
            >
              <path d="M21 15v4a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2v-4" />
              <polyline points="7 10 12 15 17 10" />
              <line x1="12" y1="15" x2="12" y2="3" />
            </svg>
          </button>
          <button
            class="bg-indigo-500 hover:bg-indigo-400 text-white font-semibold mt-5 py-2 px-4 border-b-4 border-indigo-700 hover:border-indigo-500 rounded w-5/6"
          >Update Chart</button>
        </div>
      </div> -->
    </div>
    <div class="w-3/4 p-5">
      <div class="bg-white rounded shadow-lg">
        <div id="chart"></div>
      </div>
    </div>
  </div>
</template>

<script>
import { Chart } from "frappe-charts/dist/frappe-charts.min.esm";
import AxisChart from "@/configurators/AxisChart"
import BarChart from "@/configurators/BarChart"
import LineChart from "@/configurators/LineChart"
import Options from "@/controls/Options"
import Title from "@/components/Title"

const chartComponents = {
  'axis-mixed': AxisChart,
  'bar': BarChart,
  'line': LineChart
}

export default {
  name: "app",
  components: {
    Title: Title,
    Options: Options,
    AxisChart: AxisChart,
    BarChart: BarChart,
    LineChart: LineChart
  },
  data() {
    return {
      chartType: 'axis-mixed',
      currentComponent: AxisChart,
      chartTypes: [
        {label: "Axis", value: "axis-mixed"},
        {label: "Bar", value: "bar"},
        {label: "Line", value: "line"},
      ]
    }
  },
  methods: {
    updateChart(config) {
      window.chart = new Chart("#chart", config);
    },
    changeComponent(chartType) {
      this.currentComponent = chartComponents[chartType]
    }
  },
};
</script>

<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>
