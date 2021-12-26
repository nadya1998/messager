<template>
	<div class="main">
		<!-- <form method="post">
			<label for="log">Логин </label><br>
			<input name="log" type="text" placeholder="Введите логин"><br><br>
			<label for="pass">Пароль </label><br>
			<input тname="pass" type="password" placeholder="Введите пароль" v-model="password"><br><br>
			<input type="submit" value="Ввести">
		</form> -->
		<div>
			<message v-for="(message, i) in messages"
				v-bind:key="i"
				v-bind="message"/>
		</div>
		<form @submit="onSubmit">
			<input type="text" v-model="message">
			<input type="submit" v-show="message != ''">
		</form>
	</div>
</template>

<style>

</style>

<script>

import Message from './message.vue';

export default {

	watch: {
		id(newID, oldID) {
			if (newID !== oldID) {
				window.socket.send(JSON.stringify({
					action: 'DISCONNECT_FROM_CHAT',
					data: { chatID: oldID }
				}));
				window.socket.send(JSON.stringify({
					action: 'CONNECT_TO_CHAT',
					data: { chatID: newID }
				}));
				window.socket.send(JSON.stringify({
					action: 'GET_MESSAGES',
					data: { chatID: newID }
				}));
			}
			console.log(newID, oldID);
			return newID;
		}
	},

	props: [ 'id' ],

	data() {
		return {
			message: '',
			messages: [],
			password: 'somepassword'
		};
	},
	
	created() {
		// Вызывает при создании объекта
	},

	mounted() {

		console.debug('mounted');

		if (window.socket === undefined) {
			window.socket = new WebSocket('ws://' + location.hostname + ':8000');
		}

		window.socket.onopen = () => {
			window.socket.send(JSON.stringify({
				action: 'CONNECT_TO_CHAT',
				data: { chatID: this.id }
			}));
			window.socket.send(JSON.stringify({
				action: 'GET_MESSAGES',
				data: { chatID: this.id }
			}));
		};

		window.socket.onmessage = (e) => {
			let json = JSON.parse(e.data);
			let data = json.data;
			let action = json.action;
			switch(action) {
				case 'NEW_MESSAGE': {
					let message = {
						from: 'Initiated',
						time: new Date().toTimeString().substring(0, 5),
						message: data.text
					};
					this.messages.push(message);
				} break;
				case 'GET_MESSAGES': {
					this.messages = data.messages.map(text => {
						return {
							from: 'Some animal',
							time: new Date().toTimeString().substring(0, 5),
							message: text
						};
					});
				} break;
			}
		};

	},
	
	components: {
		Message: Message
	},

	methods: {
		onSubmit(e) {
			e.preventDefault();
			if (this.message === '') {
				return false;
			}
			this.publishMessage(this.message);
			this.message = '';
			return false;
		},

		reconnectToChat() {
			window.socket.send(JSON.stringify({
				action: 'CONNECT_TO_CHAT',
				data: { chatID: this.id }
			}));
		},

		async encryptMessage(text) {
			const message = await openpgp.createMessage({ 
				text: text 
			});
			const encrypted = await openpgp.encrypt({
				message,
				passwords: [ this.password ]
			});
			return encrypted;
		},

		async decryptMessage(encrypted) {
			const encryptedMessage = await openpgp.readMessage({
				armoredMessage: encrypted
			});
			const { data: decrypted } = await openpgp.decrypt({
				message: encryptedMessage,
				passwords: [ this.password ],
				format: 'text'
			});
			return decrypted;
		}, 
		
		publishMessage(text) {
			let m = {
				from: 'Me',
				time: new Date().toTimeString().substring(0, 5),
				message: text
			};

			window.socket.send(JSON.stringify({
				action: 'NEW_MESSAGE',
				data: {
					chatID: this.id,
					text: m.message 
				}
			}));
			this.messages.push(m);
		}
	}
};
	
</script>

