<template>
	<form class="form__wrapp" @submit.prevent>
		<h3>Додати користувача</h3>
		<my-input v-model="user.first_name" placeholder="Імʼя" />
		<my-input inputType="email" v-model="user.email" placeholder="Email" />
		<p class="error" v-if="error">{{ error }}</p>
		<my-button style="margin-top: 15px" @click="createUser">Додати</my-button>
	</form>
</template>

<script>
export default {
	data() {
		return {
			user: {
				first_name: "",
				email: "",
			},
			error: "",
		};
	},
	methods: {
		validate() {
			if (!this.user.first_name) {
				this.error = "Ім'я є обов'язковим.";
				return false;
			}
			if (!this.user.email) {
				this.error = "Email є обов'язковим.";
				return false;
			}

			if (!/\S+@\S+\.\S+/.test(this.user.email)) {
				this.error = "Email не вірний.";
				return false;
			}
			this.error = "";
			return true;
		},

		createUser() {
			if (this.validate()) {
				this.user.id = Date.now();
				this.$emit("create", this.user);
				this.user = {
					first_name: "",
					email: "",
				};
			}
		},
	},
};
</script>

<style>
.form__wrapp {
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: center;
}

.error {
	color: red;
	padding-top: 10px;
	font-weight: bold;
}
</style>
