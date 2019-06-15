<template>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'home',
  data () {
    return {
      intelVal: null
    }
  },
  components: {
    HelloWorld
  },
  mounted () {
    const webSocketUrl = 'ws://127.0.0.1:8000'
    const ws = new WebSocket(webSocketUrl)
    const _this = this
    ws.onopen = function () {
      console.log('imageSocketOpen')
    }
    ws.onmessage = function (ev) {
      _this.$store.dispatch('setModulesRes', JSON.parse(ev.data))
    }
    ws.onclose = function (evt) {
      console.log('imageSocketClosed!')
    }
    ws.onerror = function (evt) {
      console.log('imageSocketError!')
    }
  }
}
</script>
