<template>
	<div class="messager">
  		<div class="messager_title">
  			<div class="messager_title-text"><h1>Завайте ваши вопросы</h1></div>
  			<div class="messager_title-close" @click="messager_title_close">
  				<img src="../assets/close.svg">
  			</div>
  		</div>
  		<div class="messager_main">
        <div class="question_name" v-if="question_block_status == true">
          <div class="message_block-title">Введите тему вопроса:</div>
          <div class="quest_block">
            <input type="text" placeholder="Введите сообщение" class="input_quest" v-model="question">
            <div class="quest_button" v-on:click="question_add">Готово</div>
          </div>
          <div class="question_error" v-if="question_error_status == true">
            <div class="message_block-title quest_error"><span>Ошибка: Нельзя оставлять поле пустым</span></div>
          </div>
        </div>
  			<div class="messager_left">
          <div v-for='(chat, index) in chats'>
    				<div class="message_block">
    					<div class="message_block-time">13 окт.</div>
    					<div class="message_block-title">{{ chat.quest }}</div>
    					<div class="message_block-suptitle">Менеджер Антон</div>
    				</div>
          </div>
  				<!--<div class="message_block">
  					<div class="message_block-time">23 окт.</div>
  					<div class="message_block-title">Предложение по интегра...</div>
  					<div class="message_block-suptitle">Менеджер Татьяна</div>
  				</div>
  				<div class="message_block">
  					<div class="message_block-time">5 сен.</div>
  					<div class="message_block-title">Как узнать стоимость авто</div>
  					<div class="message_block-suptitle">Менеджер Василий</div>
  				</div>
  				<div class="message_block">
  					<div class="message_block-time">9 ноя.</div>
  					<div class="message_block-title">Калькуляция Lada</div>
  					<div class="message_block-suptitle">Менеджер Людмила</div>
  				</div>-->
  				<div class="message_add" v-on:click="message_add">
  					<img src="../assets/add.png">
  				</div>
  			</div>
  			<div class="messager_right">
  				<div class="message_status">
  					<span>Чат создан</span>
  				</div>
  				<div class="message_time">
  					13 октября 2020 г.
  				</div>
  				<div class="message-1">
					<div class="message_nick">Менеджер AutoExpenses</div>
					<div class="message_message_1">Здравствуйте, можете задавать любые вопросы, возникающие по теме авто</div>
					<div class="message_time_main">20:27</div>
  				</div>
  				<div class="message-2">
					<div class="message_message_2">Здравствуйте, интересует возможность произвести калькуляцию затрат на мой автомобиль Hyundai Solaris 2018 г. выпуска </div>
					<div class="message_time_main">20:27</div>
  				</div>
  				<form>
  				<div class="message_input">
  					<input type="text" placeholder="Введите сообщение" class="messagerr" v-model="letter_text">
  					<div class="messagerr" v-on:click="letter"></div>
  				</div>
  				</form>
  			</div>
  		</div>
  	</div>
</template>
<style>
  .quest_error span{background-color: rgba(220, 20, 60, 0.6); color: white;}
  .question_title {display: flex; align-items: center;}
  .quest_block {display: flex; align-items: center;}
  .question_name {width: 450px; height: 130px; background-color: #ADD8E6; border-radius: 0px 0px 6px 0px; position: absolute; top: 0; left: 0; z-index: 5; border: 2px solid #0066CC;}
  .quest_button {font-family: 'Proxima Nova Rg'; font-size: 22px; color: white; font-weight: 300; background-color: #0066CC; border: 2px solid #0066CC; padding: 5px 5px; margin-left: 10px; cursor: pointer;}
	.messager {width: 1077px; height: 740px; background-color: white; border-radius: 6px 6px 0px 0px; border: 1px solid #0066CC;}
	.messager_title {width: 100%; height: 62px; background-color: #0066CC; display: flex; align-items: center; padding: 0 26px; justify-content: space-between;}
	.messager_title-text h1 {font-family: 'Proxima Nova Rg'; font-size: 22px; color: white; font-weight: 300;}
	.messager_title-close {cursor: pointer;}
	.messager_left {width: 334px; border-right: 2px solid #F0F1F4; height: 676px; position: relative;}
	.messager_right {width: 741px; height: 676px; display: block; padding: 0 48px; position: relative;}
	.message_block {width: 100%; height: 67px; transition: all 0.1s linear; position: relative;}
	.message_block:hover {background-color: #F0F1F4; cursor: pointer;}
	.message_block-title {font-family: 'Proxima Nova Rg'; font-size: 18px; color: black; font-weight: 300; padding: 11px 26px;}
	.message_block-suptitle {font-family: 'Proxima Nova Rg'; font-size: 14px; color: #93989D; font-weight: 300; padding-left: 26px; margin-top: -6px;}
	.message_block-time {font-family: 'Proxima Nova Rg'; font-size: 14px; color: #93989D; font-weight: 300; position: absolute; top: 12px; right: 8px;}
	.message_add {position: absolute; bottom: 28px; right: 14px; cursor: pointer;}
	.message_status {font-family: 'Proxima Nova Rg'; font-size: 14px; color: #93989D; font-weight: 300; text-align: center; margin-top: 40px;}
	.message_status span {padding: 8px 8px; background-color: #F0F0F0; border-radius: 6px;}
	.message_time {font-family: 'Proxima Nova Rg'; font-size: 16px; color: #93989D; font-weight: 300; text-align: center; margin-top: 20px;}
	.messager_main {display: flex; position: relative; z-index: 2;}
	.message-1 {width: 400px; height: 92px; background-color: #F0F0F0; border-radius: 12px 12px 12px 0px; position: relative; margin-top: 24px; float: left;}
	.message_nick {font-family: 'Proxima Nova Rg'; font-size: 16px; color: #0066CC; font-weight: 300; padding: 18px;}
	.message_message_1 {font-family: 'Proxima Nova Rg'; font-size: 14px; color: #7C8793; font-weight: 300; padding-left: 18px; margin-top: -12px;}
	.message_time_main {font-family: 'Proxima Nova Rg'; font-size: 12px; color: #7C8793; font-weight: 300; position: absolute; bottom: 12px; right: 10px;}
	.message-2 {width: 400px; height: 92px; background-color: #e6f0fa; border-radius: 12px 12px 0px 12px; position: relative; margin-top: 26px; float: right;}
	.message_message_2 {font-family: 'Proxima Nova Rg'; font-size: 14px; color: #7C8793; font-weight: 300; padding-left: 18px; height: 92px; display: flex;align-items: center;}
	.message_input {position: absolute; bottom: 0; left: 50%; transform: translate(-50%, -50%); border-radius: 2px; border: 2px solid #D7DEE9; display: flex; align-items: center; padding-right: 13px;}
	input[type="text"].messagerr {width: 645px; outline: none; font-family: 'Proxima Nova Rg'; font-weight: normal; font-size: 18px; color: #7C8793; color: black; padding: 0 13px; -webkit-appearance: none; border: 0;}
  input[type="text"].input_quest {width: 300px; outline: none; font-family: 'Proxima Nova Rg'; font-weight: normal; font-size: 18px; color: #7C8793; color: black; padding: 0 13px; -webkit-appearance: none; border: 0; height: 40px; margin-left: 25px;}
	div.messagerr {width: 16px; height: 11px; border: none; background: url(../assets/icon.png) no-repeat; cursor: pointer;}
</style>
<script>
  import { bus } from '../main'
  import axios from 'axios'
  export default {
    data() {
      return {
        messager_title_close_value: -1,
        user_email_get: '',
        chats: [],
        question_block_status: false,
        question: '',
        question_error_status: false,
        letter_text: ''
      }
    },
    methods: {
      messager_title_close() {
        bus.$emit('messager_title_close', this.messager_title_close_value)
      },
      message_add() {
        this.question_block_status = true
      },
      question_add() {
        if (this.question != '') {
          console.log('заходит в блок')
          this.question_error_status = false,
          this.question_block_status = false,
          this.chats.push({
            quest: this.question
          });
          this.question = ''
          axios
            .get('http://service.auto.xsph.ru/new_chat?email=123')
            .then(response => {
              console.log(response)
            })
          axios
            .get('http://service.auto.xsph.ru/load_chats')
            .then(response => {
              console.log('вот тут начинается chats/load')
              console.log(response)
            })
        } else {this.question_error_status = true}
      },
      letter() {
        if (this.letter_text != '' ) {
          axios.post('/message',{
            message: this.letter_text,
            chat_id:2
          });
        }
      }
    },
    created() {
      console.log('креатед вызвался')
    }
  }
</script>