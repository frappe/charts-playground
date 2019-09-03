<template>
  <div class="flex mb-4 p-10">
    <div
      class="w-1/4 flex flex-col justify-between bg-white rounded overflow-hidden min-h-full shadow-lg p-5"
    >
      <div>
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
      <div>
        <div class="flex flex-wrap -mx-3 mb-4">
          <div class="w-full px-3">
            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">Title</label>
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              placeholder="My Awesome Chart"
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
              class="appearance-none block w-full bg-gray-200 text-gray-700 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
              id="grid-first-name"
              type="text"
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
              id="grid-last-name"
              type="number"
              placeholder="70"
            />
          </div>
        </div>
        <div class="flex flex-wrap -mx-3 mb-4">
          <div class="w-full md:w-1/3 px-3 mb-4 md:mb-0">
            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">Label</label>
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white"
              id="grid-first-name"
              type="text"
              placeholder="Region"
            />
          </div>
          <div class="w-full md:w-1/3 px-3">
            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">Start</label>
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              id="grid-last-name"
              type="number"
              placeholder="-10"
            />
          </div>
          <div class="w-full md:w-1/3 px-3">
            <label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">End</label>
            <input
              class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
              id="grid-last-name"
              type="number"
              placeholder="50"
            />
          </div>
        </div>
      </div>
      <button
        class="bg-indigo-500 hover:bg-indigo-400 text-white font-semibold mt-5 py-2 px-4 border-b-4 border-indigo-700 hover:border-indigo-500 rounded w-full"
      >Update Chart</button>
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
    const chart = new Chart("#chart", {
      title: "My Awesome Chart",
      data: this.chartData,
      type: "axis-mixed", // or 'bar', 'line', 'scatter', 'pie', 'percentage'
      height: 300,
      colors: ["#7cd6fd", "#743ee2"]
    });
  }
};
</script>

<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>
