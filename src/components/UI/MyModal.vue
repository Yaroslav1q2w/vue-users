<template>
	<div class="modal" v-if="show" @click="hideModal">
		<div class="modal__content" @click.stop>
			<slot></slot>
		</div>
	</div>
</template>

<script>
export default {
	name: "my-modal",
	props: {
		show: {
			type: Boolean,
			default: false,
		},
	},

	methods: {
		hideModal() {
			this.$emit("update:show", false);
		},
	},
};
</script>

<style>
.modal {
	height: 100%;
	width: 100%;
	position: fixed;
	top: 0;
	left: 0;
	background-color: rgba(0, 0, 0, 0.6);
	display: flex;
	justify-content: center;
	align-items: center;
	z-index: 10;
}

.modal__content {
	margin: 0 auto;
	font-style: normal;
	background-color: #fff;
	max-width: 400px;
	padding: 20px;
	width: 100%;
	z-index: 1;
	text-align: center;
	margin: 0 10px;
}
</style>
