<template>
	<div class="header__shadow">
		<div class="wrapper">
			<header>
				<div class="header__logo">AutoExpenses</div>
				<nav class="header__nav">
					<router-link to="/CostsPage"><a href="#" class="nav__link">Учет расходов</a></router-link>
					<router-link to="/CalculatorPage"><a href="#" class="nav__link">Калькулятор</a></router-link>
					<router-link to="/MapPage"><a href="#" class="nav__link">Мои путешествия</a></router-link>
				</nav>
				<div class="header__right">
					<div>
						<span class="nav__link">{{ user_name }},</span>
					</div>
					<div v-on:click="logout" class="nav__link-logout"><a class="nav__link">Выход</a></div>
					<!--<router-link to="/" class="nav__link nav__link-register"><p>Регистрация</p></router-link>-->
				</div>
			</header>
		</div>
	</div>
</template>
<style scoped>
	a {text-decoration: none;}
</style>
<style>
	@import url('https://fonts.googleapis.com/css2?family=Roboto+Condensed&display=swap');

	.wrapper {width: 1200px;margin: 0 auto;}
	header {display: flex; align-items: center; justify-content: space-between; height: 100px;}
	.header__nav {display: flex; font-family: 'Roboto Condensed', sans-serif; font-weight: 400; font-size: 18px; color: #2E2D57;}
	.header__nav a {margin-right: 25px;}
	.header__nav a:last-child {margin-right: 0;}
	.header__right {display: flex; align-items: center;}
	.nav__link{margin-left: 5px; font-family: 'Proxima Nova Rg'; font-weight: normal;}
	.header__right a:first-child{margin-left: 0px;}
	.header__logo {font-size: 28px; color: #2D2D57; font-family: 'Proxima Nova Lt'; font-weight: 600; cursor: pointer;}
	.header__right .nav__link {font-size: 18px; color: #2E2D57; font-family: 'Proxima Nova Rg'; font-weight: normal;}
	.nav__link p {border: 2px solid #0066CC; padding: 16px 32px;}
	.nav__link-register {transition: all 0.1s linear;}
	.nav__link-register:hover {background-color: #0066CC; color: white;}
	.header__shadow {box-shadow: 0 5px 5px -5px #333; width: 100%;}
	.header_right div span {display: flex; font-family: 'Roboto Condensed', sans-serif; font-weight: 400; font-size: 18px; color: #2E2D57;}
	.nav__link-logout {margin-left: 5px; cursor: pointer;}
</style>
<script>
	import axios from 'axios'
	export default {
		data() {
			return {
				user_name: ''
			}
		},
		methods: {
			logout() {
				axios
			      .get('http://service.auto.xsph.ru/logout')
			      .then(response => {
			      	console.log(response)
			      	this.$router.push('/')
			      })
			}
		},
		created() {
			axios
      			.get('http://service.auto.xsph.ru/init')
			     .then(response => {
			     	console.log(response.data.user.name)
			        this.user_name = response.data.user.name
			    })
			/*this.$store.commit('getusername'),
			this.user_name = this.$store.state.username
			if (this.user_name == '') {this.user_name = 'Не пришло'}
			console.log('В Header пришло: ' + this.$store.state.username)*/
		}
	}
</script>