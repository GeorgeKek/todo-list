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
			/>
			<div class="list">
				<div
					v-for="item in items"
				>
					<single-item
						v-if="item.date == day"
						:item="item"
						:key="item.id"
						@edit="editItem"
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
		}
	},
	data() {
		return {
			distinctDates: [],
		}
	},
	methods: {
		findDates() {
			for (let i = 0; i < this.items.length; i++)
				if (this.distinctDates.indexOf(this.items[i].date) < 0)
					this.distinctDates.push(this.items[i].date)
		},
	},
	mounted() {
		this.findDates();
	},
	updated() {
		this.findDates();
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
