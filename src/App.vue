<template>
	<DayList
		:items="items"
	/>
	<Button
		@click="showDialog"
	>
		Добавить задачу
	</Button>
	<Dialog
		v-model:show="dialogVisible"
	>
		<ItemForm
			@create="createItem"
			:items="items"
		/>
	</Dialog>
</template>

<script>
import DayList from '@/components/DayList.vue'
import Button from '@/components/Button.vue'
import Dialog from '@/components/Dialog.vue'
import ItemForm from '@/components/ItemForm.vue'
export default {
	components: {
		DayList,
		Button,
		ItemForm,
		Dialog
	},
	data() {
		return {
			dialogVisible: false,
			items: [
				{id: 1, title: "Lorem nostrud eiusmod id duis est commodo elit velit Lorem aute laborum consequat exercitation aute.", date: "11.17.21", completed: false},
				{id: 2, title: "Eiusmod minim incididunt voluptate pariatur consectetur eu est culpa ipsum eiusmod ut aute reprehenderit.", date: "11.18.21", completed: false},
				{id: 3, title: "Velit amet et est tempor id nostrud dolor exercitation ut sint sit sunt aliquip Lorem.", date: "11.18.21", completed: false},
				{id: 4, title: "Incididunt adipisicing aliquip et incididunt tempor duis anim cupidatat eu do velit nisi magna.", date: "11.18.21", completed: true},
				{id: 5, title: "Lorem nostrud eiusmod id duis est commodo elit velit Lorem aute laborum consequat exercitation aute.", date: "11.19.21", completed: false},
				{id: 6, title: "Eiusmod minim incididunt voluptate pariatur consectetur eu est culpa ipsum eiusmod ut aute reprehenderit.", date: "11.19.21", completed: false},
			],
		}
	},
	methods: {
		createItem(item) {
			this.items.push(item);
			this.dialogVisible = false;
		},
		showDialog() {
			this.dialogVisible = true;
		},
	},
	mounted() {
	}
}
</script>

<style>
body
{
	background-color: #e5e5e5;
}
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: #2c3e50;
	max-width: 514px;
	width: 100%;
	background-color: #fff;
	padding: 20px;
	border-radius: 4px;
	margin-left: auto;
	margin-right: auto;
}

#nav {
	padding: 30px;
}

#nav a {
	font-weight: bold;
	color: #2c3e50;
}

#nav a.router-link-exact-active {
	color: #42b983;
}
</style>
