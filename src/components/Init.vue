<template>
  <div id="all">
    <div @click="translatetopleft('logo')">
      <img id="logo" src="@/assets/logo-Castelnuovo.png"/>
    </div>
    <div id="text">
      <vue-typed-js @onComplete="translate" :strings="['DreamingCodes', 'Lorenzo Rizzotti', 'Castelnuovo']">
        <h1 class="typing"></h1>
      </vue-typed-js>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import VueTypedJs from 'vue-typed-js'

Vue.use(VueTypedJs)

export default {
  name: 'Init',
  methods: {
    translate: function () {
      document.getElementById("text").classList.add("translate");
      document.getElementById("text").addEventListener("animationend", function (){
        document.getElementById("logo").style.display = "block";
      })
    },
    translatetopleft: function (elementid) {
      console.log(elementid)
      document.getElementById(elementid).classList.add("translatetopleft");
    }
  }
}
</script>
<style scoped>
#logo{
  position: absolute;
  left:50%;
  top: 50%;
  transform: translate(-50%, -50%);
  display: none;
  height: auto;
  animation-name: logoanim;
  animation-fill-mode: forwards;
  animation-duration: 2s;
}
@keyframes translate {
  100% {opacity: 0%}
}
@keyframes logoanim {
  0% {width: 0%}
  65% {width: 20%}
  80% {width: 10%}
  100% {width: 40%}
}
@keyframes translatetopleft {
  100% {top: 20px; left: 20px;}
}
#all {
  background-color: black;
  position: absolute;
  width: 100%;
  height: 100%;
}
h1{
  text-align: center;
  color: white;
}
.translate{
  animation-duration: 3s;
  animation-name: translate;
  animation-fill-mode: forwards;
}

#text{
  position: absolute;
  left:50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
</style>
