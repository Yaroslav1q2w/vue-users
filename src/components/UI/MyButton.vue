<template lang="">
	<button class="btn">
		<slot></slot>
	</button>
</template>

<script>
export default {
	name: "my-button",
};
</script>

<style>
.btn {
	padding: 10px 20px;
	background-color: green;
	color: #fff;
	letter-spacing: 1px;
	cursor: pointer;
	border: 1px solid teal;
	transition: 0.5s;
}

.btn:hover {
	background-color: #1b5e20;
	box-shadow: 0px 2px 4px -1px rgba(0, 0, 0, 0.2),
		0px 4px 5px 0px rgba(0, 0, 0, 0.14), 0px 1px 10px 0px rgba(0, 0, 0, 0.12);
}
</style>
