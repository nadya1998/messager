<template>
	<div class="message">
		<header><span class="time">{{ time }}</span><span class="from">{{ from }}</span></header>
		<p>{{ message }}</p>
	</div>
</template>

<style scoped>
	.message {
		background:#fff;
		margin:30px auto;
		border-radius:10px;
		padding:3px 10px;
		max-width:300px;
	}
	.message > header {
		border-bottom:1px dashed #aaf;
	}
	.message span.time {
		float:right;
	}
	.message span.from {
		color:#20a;
	}
</style>

<script>

export default {
	props: ['time', 'from', 'message'],
};
	
</script>

