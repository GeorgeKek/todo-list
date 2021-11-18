<template>
	<form @submit.prevent>
		<h4>Создание</h4>
		<input
			v-model="item.title"
			type="text"
			placeholder="Название"
		/>
		<input
			v-model="item.date"
			type="text"
			placeholder="mm.dd.yy"
		/>
		<Button
			style="align-self: flex-end; margin-top: 15px;"
			@click="createItem"
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
			}
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
			this.item.id = this.items.length+1;
			this.item.completed = false;
			this.$emit('create', this.item)
			this.item = {
				title: '',
				date: ''
			}
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
input
{
	padding: 10px;
	margin-bottom: 15px;
}
</style>