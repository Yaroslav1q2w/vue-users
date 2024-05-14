<template>
	<div class="user__details">
		<img :src="user.avatar" alt="Avatar" class="user__avatar" />
		<h2 class="user__name">{{ user.first_name }} {{ user.last_name }}</h2>
		<div class="user__desc">
			<div class="user__text">
				<span class="colored">Email:</span><span> {{ user.email }}</span>
			</div>
			<div class="user__text" v-if="!editUser">
				<span class="colored">Телефон:</span>
				<span>{{ user.phone || "___" }}</span>
			</div>
			<div class="user__text" v-if="!editUser">
				<span class="colored">Адреса:</span>
				<span>{{ user.address || "___" }}</span>
			</div>
		</div>

		<div class="user__inputs" v-if="editUser">
			<my-input inputType="tel" v-model="user.phone" placeholder="Телефон" />
			<my-input v-model="user.address" placeholder="Адреса" />
		</div>

		<my-button v-if="!editUser" @click="editUser = true">Редагувати</my-button>
		<my-button v-if="editUser" @click="saveChanges">Зберегти зміни</my-button>
	</div>
</template>

<script>
export default {
	name: "user-details",
	props: {
		user: {
			type: Object,
			required: true,
		},
	},
	data() {
		return {
			editUser: false,
		};
	},
	methods: {
		saveChanges() {
			this.editUser = false;
			this.$emit("update-user", this.user);
		},
	},
};
</script>

<style scoped>
.user__details {
	display: flex;
	flex-direction: column;
	align-items: center;
	padding: 20px;
}

.user__avatar {
	width: 100px;
	height: 100px;
	border-radius: 50%;
	object-fit: cover;
}

.user__desc {
	display: flex;
	flex-direction: column;
	align-items: start;
	padding-bottom: 20px;
}

.user__name {
	margin-top: 10px;
}
.colored {
	font-weight: bold;
	padding-right: 6px;
}

.user__text {
	padding-top: 10px;
}

.user__inputs {
	padding-bottom: 20px;
}
</style>
