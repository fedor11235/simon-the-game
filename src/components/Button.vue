<template>
	<button
		:disabled="disabled"
		:class="{
			button: true,
			button_filled: filled,
			button_hollow: hollow,
			button_disabled: disabled
			}"
		:type="type"
	>
	{{label}}
	</button>
</template>

<script>
export default {
	name: 'Button',
	props: {
		type: {
			type: String,
			default: 'submit'
		},
		label: {
			type: String,
			required: true
		},
		disabled: Boolean,
		filled: Boolean,
		hollow: Boolean
	}
}
</script>

<style lang="sass" scoped>
$primaryColor: dodgerblue

.button 
	border: none
	position: relative
	text-transform: uppercase
	padding: 10px 20px
	border-radius: 22px
	font-weight: bold 
	color: white
	text-decoration: none
	background-color: $primaryColor
	opacity: 0.6

	&:hover 
		cursor: pointer
		opacity: 1
		

.button_hollow 
	color: white
	background-color: $primaryColor
</style>