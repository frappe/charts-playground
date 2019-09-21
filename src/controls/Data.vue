<template>
	<div :class=widthClass>
	<label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">{{ label }}</label>
	<input
		class="appearance-none block w-full bg-gray-200 text-gray-700 border border-gray-200 rounded py-3 px-4 mb-3 leading-tight focus:outline-none focus:bg-white focus:border-gray-500"
		:placeholder="placeholder"
		v-model="value"
	/>
	<!-- <p class="text-gray-600 text-xs italic">Make it as long and as crazy as you'd like</p> -->
	</div>
</template>
<script>
export default {
	name: 'Data',
	props: ['label', 'placeholder', 'value', 'width'],
	watch: {
		value() {
			this.$emit('input', this.value)
		}
	},
	computed: {
		widthClass() {
			if (this.width === 'half') return 'w-full md:w-1/2 px-3 mb-4 md:mb-0'
			if (this.width === 'third') return 'w-full md:w-1/3 px-3 mb-4 md:mb-0'
			else return 'w-full px-3'
		}
	}
}
</script>