<template>
	<main>
		<nav>
			<header>Выберите чат</header>
			<template v-for="(id, i) in chatIDs">
				<input :key="'i-' + id" 
					:id="'chat-' + i"
					type="radio" 
					name="selectedChat" 
					:value="id" 
					v-model="selectedChatID">
				<label class="chat-label" :key="'l-' + id" :for="'chat-' + i" >Чат №{{i}}</label>
			</template>
		</nav>
		<Chat :id="selectedChatID" />
	</main>
</template>

<style>
	main {
		max-width:800px;
		border:1px solid #aaa;
	}
	.chat-label {
		border-right:1px solid #449;
		padding:2px 10px;
	}
</style>

<script>
import Chat from './chat.vue';

export default {
	data() {
		return {
			chatIDs: [1, 2, 3, 4],
			selectedChatID: 1
		};
	},
	components: { 
		Chat 
	}
};
	
</script>

