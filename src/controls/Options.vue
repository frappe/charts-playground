<template>
	<div :class=widthClass>
	<label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">{{ label }}</label>
		<div class="relative mb-3">
			<select
				class="block appearance-none w-full bg-gray-200 border border-gray-200 text-gray-700 py-3 px-4 pr-8 rounded leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
				v-model="value"
			>
				<option v-for="option in options" :key="option.value" :value="option.value">{{ option.label }}</option>
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
	<!-- <p class="text-gray-600 text-xs italic">Make it as long and as crazy as you'd like</p> -->
	</div>
</template>
<script>
export default {
	name: 'Options',
	props: ['label', 'options', 'value', 'width'],
	watch: {
		value() {
			console.log(this.value)
			this.$emit('input', this.value)
		}
	},
	computed: {
		widthClass() {
			if (this.width === 'full') return 'w-full'
			if (this.width === 'half') return 'w-full md:w-1/2 px-3 mb-4 md:mb-0'
			if (this.width === 'third') return 'w-full md:w-1/3 px-3 mb-4 md:mb-0'
			if (this.width === 'two-third') return 'w-full md:w-2/3 px-3 mb-4 md:mb-0'
			else return 'w-full'
		}
	}
}
</script>