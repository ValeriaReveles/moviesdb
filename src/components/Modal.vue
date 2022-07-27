<template>
	<div class="backdrop" @click.self="$emit('close')">
		<div class="modal">
			<slot></slot>
		</div>
	</div>
</template>

<script>

</script>

<style>
.modal {
	width: 30em;
	height: 25em;
	padding: 20px;
	margin: 200px auto;
	background: linear-gradient(to bottom right, #827398, #322646);
	border-radius: 10px;
}
.backdrop {
	top: 0;
	position: fixed;
	background: linear-gradient(to bottom right, rgba(50, 38, 70,.5), rgba(230, 129, 100, .5));
	width: 100%;
	height: 100%;
}
.modal h1 {
	color: #03cfb4;
	border: none;
	padding: 0;
}
.modal p {
	font-style: normal;
}
.modal .actions {
	text-align: center;
	margin: 30px 0 10px 0;
	color: #333;
}
.modal .actions a {
	color: #333;
	padding: 8px;
	border: 1px solid #eee;
	border-radius: 4px;
	text-decoration: none;
	margin: 10px;
}
</style>