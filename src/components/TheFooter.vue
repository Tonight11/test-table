<template>
	<footer>
		<p>
			Copyright
			<a target="_blank" href="https://github.com/Tonight11">@Tonight</a>
		</p>
	</footer>
</template>

<style scoped>
	footer {
		background-color: #797cee;
		padding: 20px;
		text-align: center;
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
	}
</style>

<script>
	export default {
		props: {
			totalRecords: {
				type: Number,
				required: true,
			},
		},
	};
</script>
