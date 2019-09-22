<template>
	<div :class=widthClass>
	<label class="block uppercase tracking-wide text-gray-700 text-xs font-bold mb-2">{{ label }}</label>
	<input
		class="mr-2 leading-tight"
		type="checkbox"
		v-model="value"
	/>
	<!-- <p class="text-gray-600 text-xs italic">Make it as long and as crazy as you'd like</p> -->
	</div>
</template>
<script>
export default {
	name: 'Data',
	props: ['label', 'value', 'width'],
	watch: {
		value() {
			console.log(this.value)
			this.$emit('input', this.value)
		}
	},
	computed: {
		widthClass() {
			if (this.width === 'full') return 'w-full px-3'
			if (this.width === 'half') return 'w-full md:w-1/2 px-3 mb-4 md:mb-0'
			if (this.width === 'third') return 'w-full md:w-1/3 px-3 mb-4 md:mb-0'
			if (this.width === 'two-third') return 'w-full md:w-2/3 px-3 mb-4 md:mb-0'
			if (this.width === 'fourth') return 'w-full md:w-1/4 px-3 mb-4 md:mb-0'
			if (this.width === 'fifth') return 'w-full md:w-1/5 px-3 mb-4 md:mb-0'
			else return 'w-full md:w-1/3 px-3 mb-4 md:mb-0'
		}
	}
}
</script>