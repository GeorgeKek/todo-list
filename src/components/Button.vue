<template>
	<button class="btn">
		<slot></slot>
	</button>
</template>

<script>
export default {
	name: 'Button',
}
</script>

<style scoped>
.btn
{
	width: 100%;
	background: #27AE60;
	border-radius: 4px;
	padding: 15px 0;
	border: none;
	outline: none;
	font-family: sans-serif;
	font-style: normal;
	font-weight: normal;
	font-size: 16px;
	line-height: 19px;
	color: #FFFFFF;
	transition: 0.2s;
}
.btn:hover
{
	background-color: #166236;
	cursor: pointer;
	transition: 0.2s;
}
</style>
