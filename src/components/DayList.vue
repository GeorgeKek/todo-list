<template>
	<div
		v-if="items.length > 0"
	>
		<div
			class="days"
			v-for="day in distinctDates"
		>
			<Date
				:distinctDay="day"
				@click="newItem"
			/>
			<div class="list">
				<div
					v-for="item in items"
				>
					<single-item
						v-if="item.date == day"
						:item="item"
						:key="item.id"
						@remove="$emit('remove', item)"
						@find="$emit('find')"
					/>
				</div>
			</div>
		</div>
	</div>
	<h2 v-else style="color: red">
		Список задач пуст
	</h2>
</template>

<script>
	import Date from '@/components/Date.vue'
	import SingleItem from '@/components/SingleItem.vue'
	export default {
		components: {
			Date,
			SingleItem
		},
		props: {
			items: {
				type: Array,
				required: true,
			},
			distinctDates: {
				type: Array,
				required: true,
			}
		},
		methods: {
			newItem() {
				console.log('new');
			}
			// dropItems() {
			// 	const zone = document.querySelector('#zone');
			// 	const item = document.querySelector('')
			// }
		}
	}
</script>

<style scoped>
	.list
	{
		list-style-type: none;
		padding-left: 0;
		margin-bottom: 30px;
	}
</style>
