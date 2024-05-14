<template>
	<input
		:type="inputType"
		:value="modelValue"
		@input="updateInput"
		class="input"
	/>
</template>

<script>
export default {
	name: "my-input",
	props: {
		modelValue: {
			type: String,
			default: "",
		},
		inputType: {
			type: String,
			default: "text",
		},
	},
	methods: {
		updateInput(event) {
			this.$emit("update:modelValue", event.target.value);
		},
	},
};
</script>

<style scoped>
.input {
	width: 100%;
	border: 1px solid teal;
	padding: 10px 15px;
	margin-top: 15px;
}
</style>
