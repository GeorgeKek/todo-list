<template>
	<div
		class="item"
		draggable="true"
	>
		<label
			class="checkbox-label"
			@change="completeItem"
		>
			<input
				type="checkbox"
				class="checkbox"
				v-model="item.completed"
			>
			<span></span>
		</label>
		<span :class="['item__title', { 'through': isCheck}]" @click="showEditor">{{ item.title }}</span>
		<textarea
			type="text"
			class="input"
			v-model="item.title"
			@keydown.enter="editItem"
			@keydown.esc="cancelEdit"
			@blur="hideEditor"
		>
		</textarea>
	</div>
</template>

<script>
	export default {
		data() {
			return {
				itemCash: '',
				isKey: false,
			}
		},
		props: {
			item: {
				type: Object,
				required: true,
			}
		},
		methods: {
			completeItem(event) {
				let textEl = event.target.parentNode.nextSibling;
				if (event.target.checked)
					textEl.classList.add('through')
				else
					textEl.classList.remove('through')
				this.$emit('find');

			},
			showEditor(event) {
				if (!(event.target.classList.contains('through')))
				{
					event.target.classList.add('item__title--hide');
					event.target.nextSibling.classList.add('input--show');
					event.target.nextSibling.focus();
					this.itemCash = event.target.textContent;
					event.target.nextSibling.value = this.itemCash;
					this.isKey=false;
				}
			},
			hideEditor(event) {
				if (this.isKey == false)
				{
					if (event.target.value == '')
					{
						this.$emit('remove', this.item);
					}
					event.target.previousSibling.classList.remove('item__title--hide');
					event.target.classList.remove('input--show');
				}
			},
			editItem(event) {
				event.target.value = event.target.value.slice(0, -1);
				if (event.target.value == '')
				{
					this.$emit('remove', this.item);
				}
				event.target.previousSibling.classList.remove('item__title--hide');
				event.target.classList.remove('input--show');
				this.isKey=true;
			},
			cancelEdit(event) {
				event.target.previousSibling.textContent = this.itemCash;
				event.target.previousSibling.classList.remove('item__title--hide');
				event.target.classList.remove('input--show');
				this.isKey=true;

			}
		},
		computed: {
			isCheck() {
				if (this.item.completed === true)
					return true;
				else
					return false;
			}
		},
	}
</script>

<style scoped>
	.item
	{
		font-size: 14px;
		line-height: 20px;
		color: #333333;
		display: inline-block;
		position: relative;
		padding-left: 42px;
		cursor: pointer;
		width: 90%;
		margin-bottom: 5px;
		min-height: 42px;
	}
	.item__title
	{
		display: block;
		position: relative;
		min-height: 42px;
		line-height: 20px;
	}
	.item__title--hide
	{
		opacity: 0;
	}
	.checkbox-label
	{
		cursor: pointer;
	}
	.checkbox
	{
		visibility: hidden;
		position: absolute;
	}
	.checkbox:not(checked) + span
	{
		display: inline-block;
		width: 24px;
		height: 24px;
		border-radius: 1px;
		background-color: #ffffff;
		border: solid 1px #e1e1e1;
		position: absolute;
		border-radius: 3px;
		left: 0;
		top: 0;
		transition: border 0.3s;
	}
	.checkbox:checked + span
	{
		transition: background 0.3s;
	}
	.checkbox:checked + span::before
	{
		content: '';
		display: inline-block;
		position: absolute;
		left: -1px;
		width: 24px;
		height: 24px;
		top: -1px;
		border-radius: 3px;
		background-color: #6FCF97;
		background-image: url('../assets/check.svg');
		background-position: center;
		background-repeat: no-repeat;
		border: 1px solid #27AE60;
	}
	.checkbox:checked + span:last-child
	{
		text-decoration: line-through;
	}
	.checkbox:checked:hover + span
	{
		border: solid 1px #dbdbdb;
	}
	.checkbox:not(checked):hover + span
	{
		border: 1px solid #dbdbdb;
	}
	.through
	{
		text-decoration: line-through;
		color: #BDBDBD;
		cursor: default;
	}
	.input
	{
		display: none;
		border: none;
		outline: none;
		resize: none;
		background-color: #f1f1f1;
		position: absolute;
		box-sizing: border-box;
		left: 40px;
		border-radius: 3px;
		top: 0;
		height: 100%;
		max-width: calc( 100% - 40px );
		width: 100%;
		padding-top: 0;
		padding-right: 0;
		font-family: Avenir, Helvetica, Arial, sans-serif;
		font-size: 14px;
		line-height: 20px;
		color: #333333;
		min-height: 42px;
	}
	.input--show
	{
		display: inline-block;
	}
</style>