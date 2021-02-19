<template>
  <div id="app">
    <Init/>
    <Presentation/>
  </div>
</template>

<script>
import Vue from 'vue'
import VueNativeSock from 'vue-native-websocket'
import Presentation from "@/components/Presentation";
import Init from "@/components/Init";


export default {
  name: 'App',
  created() {
    Vue.use(VueNativeSock, 'ws://localhost:8083/pagesocket', {
      reconnection: true, // (Boolean) whether to reconnect automatically (false)
      reconnectionDelay: 5000,
    })
  },
  components: {
    Init,
    Presentation,
  }
}
</script>

<style>
*{
  margin: 0px;
}
</style>
