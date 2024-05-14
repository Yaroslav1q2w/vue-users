<template lang="">
	<my-header></my-header>

	<div class="wrapper">
		<h2 class="title">Користувачі</h2>

		<div class="header__list">
			<my-button @click="showModalForm" style="margin: 15px 0"
				>Додати користувача</my-button
			>
			<my-input
				class="input__search"
				v-model="searchQuery"
				placeholder="Пошук"
			/>
		</div>

		<my-modal v-model:show="modalForm">
			<user-form @create="createUser" />
		</my-modal>

		<my-modal v-model:show="userDetailsModal">
			<user-details
				:user="selectedUser"
				v-if="selectedUser"
				@update-user="handleUserUpdate"
			/>
		</my-modal>

		<user-list
			v-if="!isLoading"
			:users="searchedUsers"
			@open-details="openUserDetails"
			@remove="removeUser"
		/>

		<div class="spinner__wrapp" v-else>
			<atom-spinner :animation-duration="1000" :size="150" color="teal" />
		</div>
	</div>
</template>

<script>
import UserForm from "./components/UserForm.vue";
import UserList from "./components/UserList.vue";
import MyHeader from "./components/MyHeader.vue";
import UserDetails from "./components/UserDetails.vue";

import axios from "axios";
import { AtomSpinner } from "epic-spinners";

export default {
	components: {
		UserForm,
		UserList,
		UserDetails,
		AtomSpinner,
		MyHeader,
	},

	data() {
		return {
			users: [],
			modalForm: false,
			isLoading: false,
			searchQuery: "",

			selectedUser: null,
			userDetailsModal: false,
		};
	},
	methods: {
		showModalForm() {
			this.modalForm = true;
		},

		openUserDetails(user) {
			this.selectedUser = user;
			this.userDetailsModal = true;
		},

		handleUserUpdate(updatedUser) {
			const index = this.users.findIndex(
				(userItem) => userItem.id === updatedUser.id
			);

			if (index !== -1) {
				this.users[index] = updatedUser;
			}
		},

		async fetchUsers() {
			try {
				this.isLoading = true;

				const response = await axios.get("https://reqres.in/api/users?page=1");

				console.log(response.data);
				this.users = response.data.data;
			} catch (error) {
				alert("Error");
			} finally {
				this.isLoading = false;
			}
		},

		async createUser(user) {
			try {
				const response = await axios.post("https://reqres.in/api/users", user);
				const newUser = response.data;

				this.users.push(newUser);

				this.modalForm = false;
			} catch (error) {
				alert("Error");
				this.modalForm = false;
			} finally {
				this.isLoading = false;
			}
		},

		async removeUser(userId) {
			try {
				await axios.delete(`https://reqres.in/api/users/${userId}`);

				this.users = this.users.filter((user) => user.id !== userId.id);
			} catch (error) {
				console.error("Error removing user:", error);
			}
		},
	},

	mounted() {
		this.fetchUsers();
	},

	computed: {
		searchedUsers() {
			if (this.searchQuery) {
				return this.users.filter(
					(user) =>
						user.first_name
							.toLowerCase()
							.includes(this.searchQuery.toLowerCase()) ||
						user.last_name
							.toLowerCase()
							.includes(this.searchQuery.toLowerCase())
				);
			}
			return this.users;
		},
	},
};
</script>

<style>
* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
	font-family: "Montserrat", sans-serif;
}
.wrapper {
	padding: 20px;
	max-width: 1200px;
	margin: auto;
}

.title {
	font-size: 30px;
	text-align: center;
	margin-top: 20px;
	color: green;
}

.header__list {
	display: flex;
	justify-content: space-between;
	align-items: center;
}

.input__search {
	max-width: 300px;
}

.spinner__wrapp {
	padding-top: 100px;
	display: flex;
	justify-content: center;
	align-items: center;
}
</style>
