<template>
	<div class="date">
		<span>На{{ day }}&nbsp;</span>
		<strong>{{ formatDate }}</strong>
	</div>
</template>

<script>
	export default {
		props: {
			distinctDay: {
				type: String,
				required: true
			}
		},
		data() {
			return {
				today: new Date(),
				tomorrow: new Date(),
				date: '',
				day: '',
			}
		},
		computed: {
			formatDate() {
				this.date = new Date(this.distinctDay.replace(/\./g, "-"));
				let dd = this.date.getDate();
				if (dd < 10) dd = '0' + dd;

				let mm = this.date.getMonth() + 1;
				if (mm < 10) mm = '0' + mm;

				let yy = '20' + this.date.getFullYear() % 100 + 'г';

				return dd + '.' + mm + '.' + yy;
			},
		},
		methods: {
			findDay() {
				this.today.setHours(0, 0, 0, 0);
				this.tomorrow.setHours(0, 0, 0, 0);
				this.tomorrow.setDate(this.tomorrow.getDate()+1);
				if (this.date.toDateString() == this.today.toDateString())
					this.day = ' Сегодня';
				else if (this.date.toDateString() == this.tomorrow.toDateString())
					this.day = ' Завтра';

			}
		},
		mounted() {
			this.findDay();
		}
	}
</script>

<style scoped>
	.date
	{
		margin-bottom: 16px;
	}
</style>
