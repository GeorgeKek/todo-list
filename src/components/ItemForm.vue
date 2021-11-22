<template>
	<form @submit.prevent="createItem">
		<h4 class="title">Создание</h4>
		<input
			class="input"
			v-model="item.title"
			type="text"
			placeholder="Название"
		/>
		<input
			class="input"
			v-model="item.date"
			type="text"
			placeholder="yyyy.mm.dd"
		/>
		<Button
			style="align-self: flex-end; margin-top: 15px;"
		>
			Создать
		</Button>
	</form>
</template>

<script>
	import Button from "@/components/Button.vue"
	export default {
		components: {
			Button
		},
		data() {
			return {
				item: {
					title: '',
					date: '',
				},
			}
		},
		props: {
			items: {
				type: Array,
				required: true,
			}
		},
		methods: {
			createItem() {
				this.item.id = Date.now();
				this.item.completed = false;
				this.$emit('create', this.item)
				this.item = {
					title: '',
					date: ''
				};
				this.$emit('find')
			}
		}
	}
</script>

<style scoped>
	form
	{
		display: flex;
		flex-direction: column;
	}
	.input
	{
		width: 100%;
		box-sizing: border-box;
		padding: 9px 11px;
		background-color: #F2F2F2;
		border-radius: 3px;
		border: none;
		outline: none;
		margin-bottom: 15px;
	}
	.input:focus
	{
		background-color: #e2e2e2;
	}
	.title
	{
		margin-top: 0;
	}
</style>