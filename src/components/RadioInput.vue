<template>
	<div class="radioButtonsWrap">
		<p v-if="isRequired"
			:class="{
				requiredAlert: true,
				requiredAlert_error: didSubmitAttempt &&
					!value
			}">
		</p>
		<div class="buttonsWrap"
			:class="{
				'buttonsWrap_flex-row': flex_row,
				'buttonsWrap_flex-column': flex_column
			}"
		>
			<label v-for="button in buttons"
				:disabled="disabled"
				tabindex="0"
				@keyup.enter="updateInputData(button.name)"
				:key="button.name"
				:for="button.name"
				:class="{
					label: true,
					label_disabled: disabled,
					label_error: isRequired &&
						didSubmitAttempt && !value
				}"
			>
				{{button.nameLocale}}
				<input class="button" type="radio"
					:disabled="disabled"
					tabindex="-1"
					:name="name" :value="button.name"
					:id="button.name"
					:checked="button.name === value"
					@change="updateInputData($event.target.value)"
				/>
			</label>
		</div>
	</div>
</template>

<script>
export default {
	name: 'RadioInput',
	props: {
		flex_row: Boolean,
		flex_column: Boolean,
		disabled: Boolean,
		name: {
			type: String,
			required: true
		},
		defaultValue: {
			type: String,
			default: ''
		},
		buttons: {
			type: Array,
			required: true
		},
		isRequired: {
			type: Boolean,
			default: false
		},
		didSubmitAttempt: {
			type: Boolean,
			default: false
		}
	},
	data() {
		return {
			value: this.defaultValue
		}
	},
	methods: {
		updateInputData(value) {
			this.value = value;
			this.$emit('update-input-data', value)
		}
	}
}
</script>

<style lang="sass" scoped>
$primaryColor: dodgerblue

.radioButtonsWrap 
		
	.buttonsWrap 
		display: flex
		&_flex-row 
			flex-direction: row
		
		&_flex-column 
			flex-direction: column
		
		gap: 10px
		.label 
			cursor: pointer
			display: flex 
			align-items: center
			color: $primaryColor
			opacity: 0.6
			.button 
				cursor: inherit
				-webkit-appearance: unset
				margin: 0 10px 0 0
				display: block
				position: relative
				height: 20px
				width: 20px
				outline: none
				order: -1
				&::before 
					cursor: inherit
					content: ''
					display: inherit
					margin-right: 10px
					width: 18px 
					height: 18px
					border: 1px solid transparentize($primaryColor, 0.75)
					border-radius: 10px
				
				&:checked::before 
					border-color:$primaryColor
				
				&:checked::after 
					content: ''
					display: inherit
					position: absolute
					cursor: inherit
					width: 12px
					height: 12px
					background-color: $primaryColor
					border-radius: 50%
					top: calc(50% - 6px)
					right: calc(50% - 6px)		
</style>