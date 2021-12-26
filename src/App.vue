<template>
  <!-- <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/about">About</router-link>
  </div>
  <router-view/> -->
  <!-- <textarea v-model="message"></textarea> -->
  <div>
    <input type="checkbox" id="hide-all-panels" maxlength="0" class="hide-all-panels-focus move-offscreen">
    <input type="checkbox" id="show-left-panel" maxlength="0" class="left-panel-focus move-offscreen">
    <input type="checkbox" id="show-right-panel" maxlength="0" class="right-panel-focus move-offscreen">   

    <header>
        <div style="max-width:800px;margin:auto">
            <label for="show-left-panel" class="control-btn show-left-panel-btn" style="float:left">&#9776;</label>
            <h1>Шапка</h1>
            <label for="show-right-panel" class="control-btn show-right-panel-btn"  style="float:right">&#9881;</label>
        </div>
    </header>

    <nav class="panel left">
        <label class="back-btn" for="hide-all-panels" style="float:right"><div class="arrow-left"></div></label>
        <h2 id="m" class="main">Чаты</h2>
        <div class="div">
            <p class="menu"><img src="image/user.jpg" width="20px"> Чат 1</p>
            <p class="menu"><img src="image/user.jpg" width="20px"> Чат 2</p>
            <p class="menu"><img src="image/user.jpg" width="20px"> Чат 3</p>
            <p class="menu"><img src="image/user.jpg" width="20px"> Чат 4</p>
            <p class="menu"><img src="image/user.jpg" width="20px"> Чат 5</p>
        </div>
        <form method="post" class="f">
          <label for="log">Логин </label><br>
          <input name="log" type="text" placeholder="Введите логин"><br><br>
          <label for="pass">Пароль </label><br>
          <input тname="pass" type="password" placeholder="Введите пароль" v-model="password"><br><br>
          <input type="button" value="Ввести">
		    </form>
        <hr>
    </nav>
    <aside id="as" class="panel right">
        <label id="" class="back-btn" for="hide-all-panels" style="float:left"><div class="arrow-right"></div></label>
        <h2 id="n" class="main">Настройки</h2><hr>
        <ul type="square">
            <li class="m1">Учётная запись</li>
            <li class="m1">Конфиденциальность</li>
            <li class="m1">Уведомления</li>
            <li class="m1">Данные и мультимедиа</li>
        </ul>
    </aside>
    <main>
        <div id="str"><big>Выберите чат или начните новую беседу</big></div>
        <Chat :id="1" />
    </main>
  </div>
  <p>{{ encryptedMessage }}</p>
  <p>{{ decryptedMessage }}</p>
  	
</template>

<script>
import * as openpgp from 'openpgp';

import Chat from '@/components/chat.vue';

export default {
  data() {
    return {
      message: 'simple message',
      encryptedMessage: '',
      decryptedMessage: '',
      password: 'some password from user'
    };
  },

  components: { 
		Chat 
	},

  methods: {

     /*  display() {
      $("#f").toggle();
      $("#div").toggle();
    } */
  }
}

    /* async encryptMessage(text) {
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
    }
  }, 

    watch: {
      message(newValue, oldValue) {
        console.log('Было' + oldValue + ' ' + newValue);
        this.encryptMessage(newValue).then(msg => {
          this.encryptedMessage = msg;
          this.decryptMessage(msg).then(text => {
            this.decryptedMessage = text;
          });
        });
      }  
    }  */
</script>

<style>
    html {
      background-image: url(https://images8.alphacoders.com/102/1026336.jpg);
      background-size:cover;
    }
    body {
      /* Поведение для больших экранов */
      max-width:1420px;
      min-height:100%;
      /* По середине по горизонтали, сверху и снизу без отступов */
      margin:0px auto;
  
      /* Для того, чтобы позиционирование 
      элементов отсчитывать от данного элемента */
      position:relative;
      overflow:auto;
      box-sizing:border-box;
      /* Контент не должен находиться под заголовком,
      поэтому сдвинем его вниз на высоту заголовка */
      padding-top:40px;

    }
    main::-webkit-scrollbar {
        width: 0;
    }
    
    /* Кнопки "меню", "настроек" и "назад" */
    .control-btn {
        display:none;
        background: rgba(0, 0, 0, 0);
        border:1px solid rgb(53, 6, 35);
        cursor:pointer;
        border-radius:50px;
        padding:5px 15px;
        width:max-content;
        box-shadow: -3px 4px 5px 1px #2b2226;
    }

    .back-btn {
        display:none;
        background: rgba(0, 0, 0, 0);
        border:1px solid rgb(53, 6, 35);
        cursor:pointer;
        border-radius:50px;
        padding:5px 10px;
        width:max-content;
        box-shadow: -3px 4px 5px 1px #2b2226;
        margin-top: 10px;
    }
        
    /* Какая-то реакция при наведении мышки */
    .control-btn:hover, 
    .back-btn:hover {
        background:rgba(243, 121, 162, 0.486);
    }
    /* Какая-то реакция при нажатии на кнопку */
    .control-btn:active, 
    .back-btn:active {
        background:rgba(243, 121, 162, 0.486);
        box-shadow: -1px 2px 2px 1px #20131d;

    }

    /* Заголовок сайта */
    body > header {
        position:fixed;
        top:0px;
        left:0px;
        right:0px;
        height:30px;
        text-align:center;
        box-shadow:0 0 10px #000;
        z-index:4000;
        padding-bottom: 6px;
    }
        
    h1 {
        font-family: Impact, fantasy;
        color: #c8afb6;
        text-shadow: 2px 2px 1px #000;
        margin:0px;
        vertical-align:middle;
        display:inline-block;
    }
        
    header {
        background-color: #3e0420;
        color:#fff;
        margin:0px;
        vertical-align:middle;
        display:inline-block;
    }
        
    /* Нужен для перемещения элементов, которые не должны быть
    видны, за область видимости экрана */
    .move-offscreen {
        position:fixed;
        bottom:110%;
        left:110%;
    }

      /* Стилизация панели (и слева и справа) */
    .panel {
        position:absolute;
        /* Отступ сверху: 2 заголовка (по 40 пикс.) и расстояния между ними (10 пикс.) */
        top:50px;
        
        /* Ширина панели */
        width:290px;
        height: 90vh;
        
        /* Если ширина экрана становится меньше ширины панели, то панель занимает весь экран */
        max-width:100%;
        
        /* Если ширина экрана становится меньше ширины панели, то панель занимает весь экран */
        padding:0px;
        box-sizing:border-box;
        
        /* Изменение стилей происходит за 0.5 секунд.
        Например, панель за столько выезжает полностью.
        Если убрать, то всё будет моментально. */
        transition:0.3s;
    }
        
    .panel.left {
        left:0px;
        
        background: linear-gradient(45deg, #2f0f21, #681e46, #7a192e);
        box-shadow: -6px 10px 5px 5px #24091b;
        border-radius: 25px;
        overflow-y: auto;
    }
        
    .panel.right {
        right:0px;
        background: linear-gradient(45deg, #2f0f21, #681e46, #7a192e);
        box-shadow: 6px 10px 5px 5px #24091b;
        border-radius: 25px;
    }

    .panel.left::-webkit-scrollbar {
        width: 0.1;
        color:violet;
    }

    .div {
        padding-left: 10px;
    }
    
    .main{
        padding-left: 20px;
        font-family: Impact, fantasy;
        color: #c8afb6;
        text-shadow: 2px 2px 1px #000;
        text-shadow: 2px 3px 3px #2c2229;
    }


        /* Основной блок. По центру body */
    main {
            /* По центру */
      display:block;
      margin: auto;
      padding-top: 250px;
      padding-left:5px;
      padding-right:5px;
      text-align: center;
      width: 820px;
      height: 91vh;
      background: linear-gradient(0deg, #500928, #500d21, #6d2238, #882543, #ae3358, #c23058);
      box-sizing: border-box;
      overflow-y: auto;
      border-radius: 25px;
      box-shadow: 0px 5px 5px 5px #24091b;
      color: #c8afb6;
      /* Максимальную ширину нужно расчитать */
      max-width:800px;
            /* Когда отступов текста от границ нет, выглядит плохо */
            /* padding:250px; */
            /* Задний фон основной области */
            /* background:#fff; */
    } 
        
    .menu {
      padding-left: 20px;
      font-family: Comic Sans MS, Comic Sans, cursive;
      color: #c8afb6;
    }

    .menu:hover {
      color: #db2959;
      text-decoration: underline;
      cursor: pointer;
      font-style: italic;
    }

    .m1 {
      font-family: Comic Sans MS, Comic Sans, cursive;
      color: #c8afb6;
    }

    #n {
      padding-left: 10px;
      font-family: Impact, fantasy;
      color: #c8afb6;
      text-shadow: 2px 2px 1px #000;
    }

    .m1:hover {
      color: #db2959;
      text-decoration: underline;
      cursor: pointer;
      font-style: italic;
    }


    .arrow-right {
      transform: rotate(45deg);
      width: 10px;
      height: 10px;
      border-top: 5px solid #3a1731;
      border-right: 5px solid #290a21;
      margin-right: 3px;

    }

    .arrow-left {
      transform: rotate(-135deg);
      width: 10px;
      height: 10px;
      border-top: 5px solid #290a21;
      border-right: 5px solid #3a1731;
      margin-left: 3px;
    }  

    @media all and (max-width:1400px) {
        
      body {
          max-width:1130px;
      }
      main {
          width:unset;
          margin-right:0px;
      }
      .panel.right {
          position:fixed;
          top:40px;    
          bottom:0px;
          z-index:5000;
          right:-310px;
      }
      #show-right-panel:focus ~ .panel.right,
      #hide-all-panels:not(:focus) ~ .panel.right:hover,
      #hide-all-panels:not(:focus) ~ .panel.right:focus-within {
          right:0px;
      }
      .panel.right .back-btn {
          display:inline-block;
      }
      .show-right-panel-btn {
          display:inline-block;
      }
      .panel.right > section {
          height:100%;
      }
    
    }
    
    @media all and (max-width:1100px) {
      main {
          margin:auto;
      }
      .panel.left .back-btn {
          display:inline-block;
      }
      .panel.left {
          position:fixed;
          top:40px;    
          bottom:0px;
          z-index:5000;
          left:-310px;
      }
      #show-left-panel:focus ~ .panel.left,
      #hide-all-panels:not(:focus) ~ .panel.left:hover,
      #hide-all-panels:not(:focus) ~ .panel.left:focus-within {
          left:0px;
      }
      .panel.left > section {
        height:100%;
      }
      .show-left-panel-btn {
        display:inline-block;
      }
    
    }
    
    .panel input, main input {
      display:block;
      width:100%;
    }
</style>