<template>
	<div class="flex m-5">
		<div
			class="w-1/4 flex flex-col justify-between bg-white overflow-hidden shadow p-5 rounded-lg"
		>
			<div class="chart-config">
				<Title />
				<Options
					label="Chart Type"
					:options="chartTypes"
					width="full"
					v-model="chartType"
				/>
				<component :is="currentComponent" @updateChart="updateChart" />
			</div>
		</div>
		<div class="w-3/4 ml-5">
			<div class="bg-white shadow p-5 rounded-lg">
				<div id="chart"></div>
			</div>
		</div>
	</div>
</template>

<script>
/* eslint-disable */
import { Chart } from "frappe-charts/dist/frappe-charts.esm";
import AxisChart from "@/configurators/AxisChart";
import BarChart from "@/configurators/BarChart";
import LineChart from "@/configurators/LineChart";
import Options from "@/controls/Options";
import Title from "@/components/Title";

export default {
	name: "app",
	components: {
		Title: Title,
		Options: Options,
		AxisChart: AxisChart,
		BarChart: BarChart,
		LineChart: LineChart,
	},
	data() {
		return {
			chartType: "bar",
			chartComponents: {
				"axis-mixed": AxisChart,
				bar: BarChart,
				line: LineChart,
			},
			chartTypes: [
				{ label: "Axis", value: "axis-mixed" },
				{ label: "Bar", value: "bar" },
				{ label: "Line", value: "line" },
			],
		};
	},
	methods: {
		updateChart(config) {
			window.chart = new Chart("#chart", config);
		},
	},
	computed: {
		currentComponent() {
			return this.chartComponents[this.chartType];
		},
	},
};
</script>

<style>
@tailwind base;
@tailwind components;
@tailwind utilities;
</style>
