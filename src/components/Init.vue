<template>
  <div id="all">
    <div id="qrcode" ref="qrcode"></div>
    <div @click="translatetopleft('logo')">
      <img id="logo" src="@/assets/logo-Castelnuovo.png"/>
    </div>
    <div id="text">
      <vue-typed-js :strings="['DreamingCodes', 'Lorenzo Rizzotti', 'Castelnuovo']" @onComplete="translate">
        <h1 class="typing"></h1>
      </vue-typed-js>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import VueTypedJs from 'vue-typed-js'
import * as QRCode from 'easyqrcodejs'

Vue.use(VueTypedJs)

export default {
  name: 'Init',
  created() {
    this.$options.sockets.onmessage = (data) => {
      let JSONized = JSON.parse(data.data)
      if (JSONized.operation === "presentator") {
        console.log("Ricevuto token presentatore")
        console.log(JSONized.arg)
        new QRCode(this.$refs.qrcode, {
          text: JSONized.arg,
          logoBackgroundTransparent: true,
          width: screen.width / 100 * 40,
          height: screen.width / 100 * 40,
          drawer: "svg"
        });
      }
    }
  },
  methods: {
    translate: function () {
      let textelement = document.getElementById("text")
      let logoelement = document.getElementById("logo")
      let qrcodeelement = document.getElementById("qrcode")

      textelement.classList.add("translate");
      textelement.addEventListener("animationend", function () {
        logoelement.style.display = "block";
      })
      logoelement.addEventListener("animationend", function () {
        qrcodeelement.style.display = "block";
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
#logo {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  display: none;
  height: auto;
  animation-name: logoanim;
  animation-fill-mode: forwards;
  animation-duration: 2s;
}

@keyframes translate {
  100% {
    opacity: 0%
  }
}

@keyframes logoanim {
  0% {
    width: 0%
  }
  32.5% {
    width: 20%
  }
  40% {
    width: 10%
  }
  50% {
    width: 40%
  }
  100% {
    width: 20%
  }
}

@keyframes translatetopleft {
  100% {
    top: 20px;
    left: 20px;
  }
}

@keyframes fadein {
  100% {
    opacity: 100%;
  }
}

#all {
  background-color: black;
  position: absolute;
  width: 100%;
  height: 100%;
}

#qrcode, svg {
  display: none;
  opacity: 0%;
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  animation: fadein;
  animation-duration: 1s;
  animation-fill-mode: forwards;
}

h1 {
  text-align: center;
  color: white;
}

.translate {
  animation-duration: 3s;
  animation-name: translate;
  animation-fill-mode: forwards;
}

#text {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
}
</style>
