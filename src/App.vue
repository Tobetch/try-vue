<template>
<div>
    <myheader></myheader>
    <p v-if="msg.length > 0">
      {{msg}}
    </p>
    <p v-else>
      no text
    </p>
    <input type="text" v-model="msg">
    <button @click="clear()">clear</button><br><br><br>
    <button @click="doFetchMabual()">fetch!!</button>

  </div>
  </template>

<script>
import myheader from './components/myheader'

export default {
  components: {
    myheader
  },
  data () {
    return {
      msg: 'Hello World!'
    }
  }, methods:{
    clear () {
      this.msg = ''
      // this.msg = 'hogehoge'
    },
    doFetchMabual () {
          fetch('http://www.geonames.org/postalCodeLookupJSON?postalcode=10504&country=US')
    .then( response => {
      return response.json()
    })
    .then( json => {
      this.msg = json.postalcodes[0].adminName1
    })
    .catch( () => {
    });
    }
  },
  created () {
    fetch('http://www.geonames.org/postalCodeLookupJSON?postalcode=10504&country=US')
    .then( response => {
      return response.json()
    })
    .then( json => {
      this.msg = json.postalcodes[0].adminName1
    })
    .catch( () => {
    });
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
