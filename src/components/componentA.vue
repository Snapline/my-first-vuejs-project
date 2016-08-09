<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <h1>{{messagefromfather}}</h1>
    <button v-on:click="onClickMe">open mouse!</button>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      msg: 'Hi from component A!'
    }
  },
  props: ['messagefromfather'],
  methods: {
    onClickMe: function(){
        console.log(this.messagefromfather);
        this.$dispatch('child-tell-me-sth', this.msg)
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  color: #42b983;
}
</style>
