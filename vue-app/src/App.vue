<template>
  <div id="app" class="reminder-container" v-cloak>
    <img class="logo" src="./assets/logo.png">
    <h1 v-text="title"></h1>
	<br/>
	<input type="text" v-model="newItem"  v-on:keyup.enter="addNew" placeholder="enter输入" />
    <ul class="reminders">
      <li v-for="item in items" v-bind:class="{isFinshed:item.isFinshed}" v-on:click="toggleFinshed(item)">
        {{ item.label }} <span class="fr">{{item.isFinshed ? "完成" : "未完成" }}</span>
      </li>
    </ul>
</div>

</template>

<script>
import Store from './components/store'
export default {
  data () {
    return {
      items: Store.fetch(),
      newItem: '',
      title: '添加自己的工作计划(vue.js)'
    }
  },
  watch: {
    items: {
      handler (items) {
        Store.save(items)
      },
      deep: true
    }
  },
  methods: {
    addNew () {
      if (this.newItem === '') {
        window.alert('不能为空')
        return
      }
      this.items.push({
        label: this.newItem,
        isFinshed: false
      })
      this.newItem = ''
    },
    toggleFinshed (item) {
      item.isFinshed = !item.isFinshed
    }
  }
}
</script>

<style>
*{
  margin:0;
  padding:0;
  -moz-box-sizing: border-box;
   -webkit-box-sizing: border-box;
  box-sizing: border-box;
}
::-webkit-input-placeholder {
  color: rgba(255, 255, 255, 0.2)
}

:-moz-placeholder {
  color: rgba(255, 255, 255, 0.2)
}

::-moz-placeholder {
  color: rgba(255, 255, 255, 0.2)
}

:-ms-input-placeholder {
  color: rgba(255, 255, 255, 0.2)
}

ol,ul,li{list-style:none;}
img{border:0 none;}
a,input,textarea{outline:none;}
.clearfix{*zoom:1;}
.clearfix:after{clear:both;content:'';display:block;height:0;visibility:hidden;}
.fr{float:left;}
.fr{float:right}

body {
     background-color: #16a085;
  font-family: "Lato", sans-serif;
  height: 2000px;
  color: white
}

.reminders {
  list-style-type: none;
  max-width: 500px;
  margin: 30px auto
}

input[type='text'] {
  width: 430px;
  height: 50px;
  border: none;
  background-color: transparent;
  font-size: 20px;
  font-weight:300;
  color: white;
  padding:5px 10px;
  -webkit-transition: all .3s ease;
  -o-transition: all .3s ease;
  transition: all .3s ease;
  background-color: rgba(0,0,0,.15);
}

.reminders {
  list-style-type: none;
  max-width: 430px;
  margin: 30px auto
}

.reminders li {
  z-index:1;
  font-weight: 400;
  /*box-shadow: 0 7px 0 -4px rgba(0, 0, 0, 0.2);*/
  color: #444;
  text-align: left;
  min-height: 50px;
  line-height: 30px;
  font-size: 20px;
  background-color: white;
  margin-bottom: 10px;
  padding: 10px;
  position: relative;

  word-wrap: break-word;
  -webkit-transition: all .1s ease;
  -o-transition: all .1s ease;
  transition: all .1s ease
}
.reminders li:focus {
  outline: none;
}

.reminders li.isFinshed{
text-decoration:line-through;
    color: green;
}

.reminder-container h1{
 text-align:center;
 margin:50px auto 20px;
}

.reminder-container input{
 margin:0 auto;
 display:block;
}

	[v-cloak]{
		display: none;
	}

.logo {
  width: 100px;
  height: 100px
}
</style>
