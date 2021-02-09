<template>
  <div id="app">
    <Init/>
  </div>
</template>

<script>
import Init from './components/Init.vue'
import Vue from 'vue'
import VueNativeSock from 'vue-native-websocket'


export default {
  name: 'App',
  created() {
    Vue.use(VueNativeSock, 'ws://localhost:8083/pagesocket', {
      reconnection: true, // (Boolean) whether to reconnect automatically (false)
      reconnectionDelay: 5000,
    })
  },
  components: {
    Init
  }
}
</script>

<style>
*{
  margin: 0px;
}
</style>
