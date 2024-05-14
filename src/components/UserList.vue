<template>
	<div class="user__list" v-if="users.length > 0">
		<transition-group name="user-list">
			<user-item
				:user="user"
				v-for="user in users"
				:key="user.id"
				@remove="$emit('remove', user)"
				@open-details="$emit('open-details', user)"
			/>
		</transition-group>
	</div>
	<h1 class="title" v-else>Список користувачів порожній</h1>
</template>

<script>
import UserItem from "./UserItem.vue";

export default {
	components: { UserItem },

	props: {
		users: {
			type: Array,
			required: true,
		},
	},

	methods: {},
};
</script>

<style scoped>
.user__list {
	display: flex;
	flex-wrap: wrap;
	justify-content: space-around;
	align-items: center;
}
.user-list-item {
	display: inline-block;
	margin-right: 10px;
}
.user-list-enter-active,
.user-list-leave-active {
	transition: all 1s;
}
.user-list-enter,
.user-list-leave-to {
	opacity: 0;
	transform: translateY(30px);
}
</style>
