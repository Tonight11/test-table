<template>
	<div class="input-container">
		<input
			:type="type"
			:id="forId"
			required=""
			:value="modelValue"
			@input="updateModelValue($event.target.value)"
		/>
		<label :for="forId" class="label">{{ text }}</label>
		<div class="underline"></div>
	</div>
</template>

<script>
	export default {
		props: {
			modelValue: {
				type: [String, Number],
				required: true,
			},
			type: String,
			text: String,
			forId: String,
		},
		emit: ['modelValue'],
		methods: {
			updateModelValue(newValue) {
				this.$emit('update:modelValue', newValue); // Отправляем событие изменения в родительский компонент
			},
		},
	};
</script>

<style scoped>
	.input-container {
		position: relative;
		margin: 50px auto;
		width: 200px;
	}

	.input-container input[type='text'] {
		font-size: 16px;
		width: 100%;
		border: none;
		border-bottom: 2px solid #ffffff;
		padding: 5px 0;
		background-color: transparent;
		outline: none;
		color: white;
	}

	.input-container .label {
		position: absolute;
		top: 0;
		left: 0;
		color: #ffffff;
		transition: all 0.3s ease;
		pointer-events: none;
	}

	.input-container input[type='text']:focus ~ .label,
	.input-container input[type='text']:valid ~ .label {
		top: -20px;
		font-size: 16px;
		color: #b6b6b6;
	}

	.input-container .underline {
		position: absolute;
		bottom: 0;
		left: 0;
		height: 2px;
		width: 100%;
		background-color: #b6b6b6;
		transform: scaleX(0);
		transition: all 0.3s ease;
	}

	.input-container input[type='text']:focus ~ .underline,
	.input-container input[type='text']:valid ~ .underline {
		transform: scaleX(1);
	}
</style>
