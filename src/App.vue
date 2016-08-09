<template>
  <div id="app">
      <h1 v-text="title"></h1>
      <label>add your list:</label><input v-model="newItem" v-on:keyup.enter="addNew" />
      <ol>
         <li v-for="item in items" v-bind:class="{finished:item.isFinished}" v-on:click="toggleFinish(item)">
           {{item.label}}
         </li>
      </ol>

      <div class="below_area">
        <p>The area below shows the data transfer from father to child and verse.</p>
        <p>child tells me: <em>{{childWords}}</em></p>
      <Component-a messagefromfather="You Die!" v-on:child-tell-me-sth='listenToMyBoy'></Component-a>
      </div>
      
  </div>
</template>

<script>
import Store from './store'
import ComponentA from './components/componentA'

export default {
  data: function(){
    return {
      title: 'This is a TO-DO list',
      items: Store.fetch(),
      newItem: '',
      childWords: ''
    }
  },
  components:{
      ComponentA
  },
  watch: {
    items: {
      handler: function(items){
        Store.save(items);
      },
      deep:true
    }
  },
  enents: {
    'child-tell-me-sth': function(msg){
      this.childWords = msg;
    }
  },
  methods: {
    toggleFinish: function(item){
      item.isFinished=!item.isFinished
    },
    addNew: function(){
      this.items.push({
        label: this.newItem,
        isFinished:false
      })
      this.newItem='';
    },
    listenToMyBoy: function(msg){
      this.childWords = msg;
    }
  }
}
</script>

<style>
.finished{
  text-decoration: underline;
}
html {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}

ol{
  width:60%;
  margin: 50px auto 0;
}

ol li{
  width:40%;
  margin: 0 auto;
}

#app {
  color: #2c3e50;
  font-family: Source Sans Pro, Helvetica, sans-serif;
  text-align: center;
}

#app a {
  color: #42b983;
  text-decoration: none;
}

.logo {
  width: 100px;
  height: 100px
}

.below_area{
  margin-top: 80px;
}

.below_area p{
  font-weight: 700
}
</style>
