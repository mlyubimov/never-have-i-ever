<template>
	<div id="app">
		<!-- <img alt="Vue logo" src="./assets/logo.png"> -->
		<transition name="fade">
			<p class="text" v-if="show">{{ this.text }}</p>
		</transition>
		<button class="btn" @click="random">
			<span>Я никогда не...</span>
		</button>
	</div>
</template>

<script>
export default {
	name: 'App',
	data () {
		return {
			text: '',
			show: false
		}
	},
	created () {
		this.random()
	},
	computed: {
		state () {
			return this.$store.state
		}
	},
	methods: {
		random () {
			this.show = false
			const max = Math.floor(this.$store.state.hot.text.length)
			this.text = this.$store.state.hot.text[Math.floor(Math.random() * max) + 1]
			setTimeout(() => {
				this.show = true
			}, 300)
		}
	}
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@600;700;900&display=swap');

* {
	margin: 0;
	padding: 0;
	box-sizing: border-box;
}

body {
	height: 100vh;
}

#app {
	display: flex;
	justify-content: space-between;
	align-items: center;
	flex-direction: column;
	height: 100%;
	padding: 250px 50px;
	font-family: Avenir, Helvetica, Arial, sans-serif;
	font-weight: 700;
	text-align: center;
	background: linear-gradient(180deg,#090020 0%,#260147 100%);
	color: #eeeeee;
	// margin-top: 60px;
}

.text {
	max-width: 60%;
	margin-bottom: 50px;
	font-family: Montserrat;
	font-size: 30px;
	line-height: 150%;
}

.btn {
	width: 25%;
	padding: 20px 100px;
	border: none;
	border-radius: 50px;
	background: linear-gradient(0deg,rgba(21,0,38,0.3),rgba(0,0,0,0)),linear-gradient(90deg,#7500ff,#be00ff,#FF14CF,#be00ff,#7500ff,#be00ff);
	background-size: cover,500% 100%;
	transition: opacity 0.15s ease-in-out;
	outline: none;

	& span {
		font-family: Montserrat;
		font-size: 22px;
		font-weight: 700;
		color: #eeeeee;
		transition: 0.15s ease-in-out;
	}

	&:hover {
		cursor: pointer;
	}

	&:active {
		padding: 20px 100px;

		& span {
			font-size: 20px;
		}
	}
}

.fade-enter-active, .fade-leave-active {
	transition: opacity .5s;
}

.fade-enter, .fade-leave-to /* .fade-leave-active до версии 2.1.8 */ {
	opacity: 0;
}

@media screen and (max-width: 500px) {
	#app {
		padding: 200px 25px 50px;
	}

	.text {
		max-width: 100%;
		font-size: 25px;
	}

	.btn {
		width: 100%;
		min-height: 62px;

		& span {
			font-size: 18px;
		}

		&:active {
			& span {
				font-size: 16px;
			}
		}
	}
}
</style>
