<template>
  <div class="flex mb-4 p-10">
    <div
      class="w-1/4 flex flex-col justify-between bg-white rounded overflow-hidden min-h-full shadow-lg p-5"
    >
      <Title/>
      <div class="chart-config">
        <div class="w-full mb-6">
          <label
            class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
            for="grid-state"
          >Chart Type</label>
          <div class="relative">
            <select
              class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              v-model="chartType"
            >
              <option value="axis-mixed">Mixed</option>
              <option value="donut">Donut</option>
              <option value="pie">Pie</option>
              <option value="percentage">Percentage</option>
            </select>
            <div
              class="pointer-events-none absolute inset-y-0 right-0 flex items-center px-2 text-gray-700"
            >
              <svg
                class="fill-current h-4 w-4"
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 20 20"
              >
                <path
                  d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
                />
              </svg>
            </div>
          </div>
        </div>
        <AxisChart @updateChart="updateChart"/>
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
            @click="createChart()"
          >Update Chart</button>
        </div>
      </div> -->
    </div>
    <div class="w-3/4">
      <div class="bg-white rounded shadow-lg px-5 pt-5 ml-5 mb-5">
        <div id="chart"></div>
      </div>
    </div>
  </div>
</template>

<script>
import { Chart } from "frappe-charts/dist/frappe-charts.min.esm";
import AxisChart from "@/configurators/AxisChart"
import Title from "@/components/Title"

export default {
  name: "app",
  components: {
    Title: Title,
    AxisChart: AxisChart
  },
  data() {
    return {
      chartType: 'axis-mixed'
    }
  },
  methods: {
    updateChart(config) {
      window.chart = new Chart("#chart", config);
    }
  }
};
</script>

<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>
