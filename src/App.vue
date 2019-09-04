<template>
  <div class="flex mb-4 p-10">
    <div
      class="w-1/4 flex flex-col justify-between bg-white rounded overflow-hidden min-h-full shadow-lg p-5"
    >
      <div id="title">
        <h1 class="text-center text-2xl font-bold">Frappe Charts Playground</h1>
        <div class="text-center mt-2">
          <a
            class="uppercase text-sm text-gray-600 hover:text-gray-800 font-bold p-2"
            href="https://github.com/frappe/charts"
          >Github</a>
          <a
            class="uppercase text-sm text-gray-600 hover:text-gray-800 font-bold p-2"
            href="https://frappe.io/charts/docs"
          >Documentation</a>
        </div>
        <hr class="bg-gray-300 h-px w-100 my-5" />
      </div>
      <div class="chart-config">
        <div class="w-full mb-6">
          <label
            class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
            for="grid-state"
          >Chart Type</label>
          <div class="relative">
            <select
              class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              v-model="chartConfig.type"
              value="chartConfig.type"
            >
              <option value="line">Line</option>
              <option value="bar">Bar</option>
              <option value="axis-mixed">Mixed</option>
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
        <div class="flex flex-wrap -mx-3 mb-4">
          <div class="w-full px-3">
            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">Title</label>
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              placeholder="My Awesome Chart"
              v-model="chartConfig.title"
            />
            <!-- <p class="text-gray-600 text-xs italic">Make it as long and as crazy as you'd like</p> -->
          </div>
        </div>
        <div class="flex flex-wrap -mx-3 mb-4">
          <div class="w-full md:w-1/2 px-3 mb-4 md:mb-0">
            <label
              class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
              for="grid-first-name"
            >Y-Marker Label</label>
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              type="text"
              v-model="chartData.yMarkers[0].label"
              placeholder="Marker"
            />
          </div>
          <div class="w-full md:w-1/2 px-3">
            <label
              class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2"
              for="grid-last-name"
            >Y-Marker Value</label>
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              type="number"
              v-model="chartData.yMarkers[0].value"
              placeholder="70"
            />
          </div>
        </div>
        <div class="flex flex-wrap -mx-3 mb-4">
          <div class="w-full md:w-1/3 px-3 mb-4 md:mb-0">
            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">Label</label>
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
              type="text"
              v-model="chartData.yRegions[0].label"
              placeholder="Region"
            />
          </div>
          <div class="w-full md:w-1/3 px-3">
            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">Start</label>
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              type="number"
              v-model="chartData.yRegions[0].start"
              placeholder="-10"
            />
          </div>
          <div class="w-full md:w-1/3 px-3">
            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">End</label>
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              type="number"
              v-model="chartData.yRegions[0].end"
              placeholder="50"
            />
          </div>
        </div>
      </div>
      <div id="controls">
        <div class="flex flex-row">
          <button
            class="bg-gray-500 hover:bg-gray-400 text-gray-200 font-semibold mt-5 mr-2 py-2 px-4 border-b-4 border-gray-700 hover:border-gray-500 rounded w-1/6"
          >
            <svg
              xmlns="http://www.w3.org/2000/svg"
              width="24"
              height="24"
              viewBox="0 0 24 24"
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
      </div>
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

export default {
  name: "app",
  data() {
    return {
      chartConfig: {
        type: "axis-mixed", // or 'bar', 'line', 'scatter', 'pie', 'percentage'
        height: 300,
        title: "My Awesome Chart"
      },
      chartData: {
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
            name: "Yet Another",
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
      }
    };
  },
  mounted() {
    this.createChart();
  },
  methods: {
    createChart() {
      window.chart = new Chart("#chart", {
        data: this.chartData,
        ...this.chartConfig
      });
    }
  }
};
</script>

<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>
