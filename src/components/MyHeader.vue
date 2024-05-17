<template lang="">
	<div class="header">
		<div class="header__inner">
			<h1 class="header__logo">Vue</h1>
		</div>
	</div>
</template>

<script>
export default {};
</script>

<style>
.header {
	box-shadow: 4px 4px 6px #ccc;
}
.header__inner {
	height: 80px;
	max-width: 1200px;
	padding: 0 10px;
	margin: 0 auto;
	display: flex;
	justify-content: space-between;
	align-items: center;
}
.header__logo {
	font-size: 34px;
	font-weight: bold;
	padding-bottom: 3px;

	color: #000;
}
</style>
