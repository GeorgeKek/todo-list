<template>
	<div class="wrap">
		<div class="sidebar">
			<input
				class="search"
				v-model="search"
				type="text"
				placeholder="Поиск..."
				@input="findDates"
			>
			<ul>
				<li>
					<span>Все задачи</span><span>{{ allItems }}</span>
				</li>
				<li>
					<span>Законченные задачи</span><span>{{ completedItems }}</span>
				</li>
			</ul>
		</div>
		<div class="main">
			<DayList
				:items="filteredItems"
				:distinctDates="distinctDates"
				@remove="removeItem"
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
					@find="findDates"
				/>
			</Dialog>
		</div>
	</div>
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
				distinctDates: [],
				search: '',
				items: [
					{id: 1, title: "Lorem nostrud eiusmod id duis est commodo elit velit Lorem aute laborum consequat exercitation aute.", date: "2021.11.18", completed: false},
					{id: 2, title: "Eiusmod minim incididunt voluptate pariatur consectetur eu est culpa ipsum eiusmod ut aute reprehenderit.", date: "2021.11.20", completed: false},
					{id: 3, title: "Velit amet et est tempor id nostrud dolor exercitation ut sint sit sunt aliquip Lorem.", date: "2021.11.19", completed: false},
					{id: 4, title: "Incididunt adipisicing aliquip et incididunt tempor duis anim cupidatat eu do velit nisi magna.", date: "2021.11.19", completed: true},
					{id: 5, title: "Lorem nostrud eiusmod id duis est commodo elit velit Lorem aute laborum consequat exercitation aute.", date: "2021.11.20", completed: false},
					{id: 6, title: "Eiusmod minim incididunt voluptate pariatur consectetur eu est culpa ipsum eiusmod ut aute reprehenderit.", date: "2021.11.20", completed: false},
					{id: 7, title: "Eiusmod minim incididunt voluptate pariatur consectetur eu est culpa ipsum eiusmod ut aute reprehenderit.", date: "2021.11.21", completed: false},
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
			removeItem(item) {
				this.items = this.items.filter(i => i.id !== item.id);
				this.findDates();
			},
			findDates() {
				this.distinctDates = [];
				for (let i = 0; i < this.filteredItems.length; i++)
					if (this.distinctDates.indexOf(this.filteredItems[i].date) < 0)
						this.distinctDates.push(this.filteredItems[i].date)
					this.distinctDates.sort();
			},
		},
		computed: {
			filteredItems() {
				const str = this.search.toLowerCase();
				return this.items.filter(item => {
					return item.title.toLowerCase().includes(str);
				});
			},
			allItems() {
				return this.items.length;
			},
			completedItems() {
				let length = 0;
				for (let i = 0; i < this.items.length; i++) {
					if (this.items[i].completed == true)
					length++;
					// console.log(length);
				}
				return length;
			}
		},
		mounted() {
			this.findDates();
		},
	}
</script>

<style>
	body
	{
		background-color: #e5e5e5;
	}
	#app
	{
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		color: #2c3e50;
		max-width: 763px;
		width: 100%;
		background-color: #fff;
		padding: 20px;
		border-radius: 4px;
		margin-left: auto;
		margin-right: auto;
	}
	.wrap
	{
		display: flex;
		justify-content: space-between;
		align-items: flex-start;
	}
	.sidebar
	{
		max-width: 218px;
		width: 100%;
		margin-right: 30px;
	}
	.main
	{
		width: 100%;
	}
	.search
	{
		width: 100%;
		box-sizing: border-box;
		padding: 9px 11px;
		background-color: #F2F2F2;
		border-radius: 3px;
		border: none;
		outline: none;
	}
	.search:focus
	{
		background-color: #e2e2e2;

	}
</style>
