<template lang="">
	<div class="user">
		<img :src="user.avatar" alt="" class="post__img" />
		<h2 @click="$emit('open-details', user)" class="user__name">
			{{ user.first_name }} {{ user.last_name }}
		</h2>
		<p class="user__email">{{ user.email }}</p>

		<my-button @click="$emit('remove', user)">Видалити</my-button>
	</div>
</template>

<script>
export default {
	props: {
		user: {
			type: Object,
			required: true,
		},
	},
};
</script>

<style scoped>
.user {
	padding: 15px;
	border: 2px solid teal;
	margin-top: 15px;
	display: flex;
	align-items: center;
	justify-content: space-between;
	flex-direction: column;
	max-width: 340px;
	width: 100%;
}

.post__img {
	border-radius: 100px;
}
.user__name {
	color: #404040;
	line-height: 1;
	margin: 0;
	cursor: pointer;
	padding-top: 16px;
	font-weight: 600;
	font-size: 24px;
	transition: 0.5s;
}
.user__name:hover {
	color: #6e6d6d;
}
.user__email {
	font-weight: 400;
	font-size: 15px;
	line-height: 1;
	letter-spacing: 0.5px;
	color: rgba(0, 0, 0, 0.6);
	padding: 16px 0 20px;
}
</style>
