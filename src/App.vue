<template>
  <div id="app">
    <div id="X" class="bar x">{{x}}</div>

    <div id="Y" class="bar y">{{y}}</div>

    <div id="Z" class="bar z">{{z}}</div>
  </div>

</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Vue from "vue"
//import VueWebsocket from "vue-websocket";
//Vue.use(Vue)
//Vue.use(VueWebsocket, "ws://192.168.8.100:8080");

import axios from 'axios'
import VueAxios from 'vue-axios'

Vue.use(VueAxios, axios)

const url = "http://192.168.8.100:8080"
//const url = "http://0.0.0.0:8080"

export default {
  name: 'app',
  data() {
    return { 
      //data: "XYZ",
      x: 1,
      y: 1,
      z: 1,
    }
  },
  components: {
    //HelloWorld
  },
  computed: {
    computedX: function () {
      return this.x;
    }
  },
  methods:{
    load() {
      axios.get(url).then(response => {
        this.x = response.data.split(',')[0]
        this.y = response.data.split(',')[1]
        this.z = response.data.split(',')[2]
      })
      //document.getElementById('X').innerHTML = this.x;
      document.getElementById('X').style["height"] = this.x + 'px';
      document.getElementById('Y').style["height"] = this.y + 'px';
      document.getElementById('Z').style["height"] = this.z + 'px';
    },
  },

  mounted: function () {
    //this.get()
    //this.load()
    this.$nextTick(function () {
      window.setInterval(() => {
        this.load()
      },100);
    })
  },
  //, render: h => h(App)
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
.bar {
  padding: 5em;
  display: inline-block;
  max-width: 30vw;
  color: white;
  font-size: 18px;
  font-weight: 800;
}
.x{
  background: red;
}
.y{
  background: green;
}
.z{
  background: blueviolet;
}
</style>
