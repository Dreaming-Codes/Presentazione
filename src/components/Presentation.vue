<template>
  <div class="solve" id="apps" style="display: none">
    <div id="whatg">
      <div id="what">
        <p class="title">What is it?</p>
      </div>
    </div>
    <div id="pecg" class="solve" style="display: none">
      <div id="pec">
        <p id="pecin" class="title">Peculiarity</p>
      </div>
      <div id="pecex" class="solve" style="display: none">
        <ul>
          <li id="remote" class="solve">Remote</li>
          <li id="multiplatform" class="solve" style="display: none">Multiplatform</li>
          <li id="animations" class="solve" style="display: none">Animations</li>
          <li id="multiuser" class="solve" style="display: none">Multiuser</li>
          <li id="user-friendly" class="solve" style="display: none">User-friendly</li>
        </ul>
      </div>
    </div>
    <div id="techg" class="solveanim" style="display: none">
      <div id="tech">
        <p id="techin" class="title">Technologies</p>
      </div>
      <div id="techexp" class="solve" style="display: none">
        <ul>
          <li id="qr" class="solve">QR Code</li>
          <li id="websocket" class="solve" style="display: none">WebSockets</li>
          <li id="cloudflare" class="solve" style="display: none">CloudFlare</li>
          <li id="internet" class="solve" style="display: none">Internet</li>
        </ul>
      </div>
    </div>
    <div id="howg" class="solveanim" style="display: none">
      <div id="how">
        <p id="howin" class="title">How did I do it?</p>
      </div>
      <div id="howexp" class="solve" style="display: none">
        <ul>
          <li id="java" class="solve">Java</li>
          <li id="js" class="solve" style="display: none">JavaScript</li>
          <li id="html" class="solve" style="display: none">HTML</li>
          <li id="css" class="solve" style="display: none">CSS</li>
        </ul>
      </div>
    </div>
    <div id="qag" class="solve" style="display: none">
      <div id="QA">
        <p class="title">Q<span style="color: orangered">&</span>A</p>
      </div>
    </div>

  </div>
</template>

<script>
// eslint-disable-next-line no-unused-vars
let currentslide = -1;

export default {
  name: "Presentation",
  created() {
    this.$options.sockets.onmessage = (data) => {
      let JSONized = JSON.parse(data.data)
      if (JSONized.operation == "step") {
        if (JSONized.arg == "next") {
          this.next()
          console.log(JSONized.arg)
        } else if (JSONized.arg == "back") {
          console.log(JSONized.arg)
        }

      }
    }
  },
  methods: {
    next: function () {
      switch (currentslide) {
        case -1:
          document.getElementById("apps").style.display = "block";
          break;
        case 0:
          document.getElementById("whatg").classList.add("dissolve");
          setTimeout(function () {
            document.getElementById("pecg").style.display = "block"
          }.bind(this), 1000)
          break;
        case 1:
          document.getElementById("pecin").classList.add("translatetotop");
          setTimeout(function () {
            document.getElementById("pecex").style.display = "block"
          }.bind(this), 1000)
          break;
        case 2:
          document.getElementById("multiplatform").style.display = "list-item"
          break;
        case 3:
          document.getElementById("animations").style.display = "list-item";
          break;
        case 4:
          document.getElementById("multiuser").style.display = "list-item";
          break;
        case 5:
          document.getElementById("user-friendly").style.display = "list-item";
          break;
        case 6:
          document.getElementById("pecg").classList.add("dissolve")
          setTimeout(function () {
            document.getElementById("techg").style.display = "block";
          }.bind(this), 1000)
          break;
        case 7:
          document.getElementById("pecg").style.display = "none";
          document.getElementById("techin").classList.add("translatetotop");
          setTimeout(function () {
            document.getElementById("techexp").style.display = "block"
          }.bind(this), 1000)
          break;
        case 8:
          document.getElementById("websocket").style.display = "list-item"
          break;
        case 9:
          document.getElementById("cloudflare").style.display = "list-item"
          break;
        case 10:
          document.getElementById("internet").style.display = "list-item"
          break;
        case 11:
          document.getElementById("techg").classList.add("dissolve");
          setTimeout(function () {
            document.getElementById("howg").style.display = "block";
          }.bind(this), 1000)
          break;
        case 12:
          document.getElementById("techg").style.display = "none";
          document.getElementById("howin").classList.add("translatetotop");
          setTimeout(function () {
            document.getElementById("howexp").style.display = "block"
          }.bind(this), 1000)
          break;
        case 13: {
          document.getElementById("js").style.display = "list-item"
          break;
        }
        case 14: {
          document.getElementById("html").style.display = "list-item"
          break;
        }
        case 15: {
          document.getElementById("css").style.display = "list-item"
          break;
        }
        case 16: {
          document.getElementById("howg").classList.add("dissolve");
          setTimeout(function () {
            document.getElementById("qag").style.display = "block";
          }.bind(this), 1000)
          break;
        }
      }
      currentslide++;
    },
    back: function () {

    }
  }
}
</script>

<style scoped>
#apps {
  position: absolute;
  height: 100%;
  width: 100%;
  background-color: black;
}

* {
  color: white;
}


@keyframes dissolveanim {
  100% {
    opacity: 0%;
  }
}

@keyframes solveanim {
  0% {
    opacity: 0%;
  }
  100% {
    opacity: 100%;
  }
}

@keyframes translatetotopanim {
  100% {
    left: 0%;
    top: 0%;
    transform: translate(0, 0);
    margin-left: 20px;
    margin-top: 10px;
  }
}

.translatetotop {
  animation-duration: 2s;
  animation-fill-mode: forwards;
  animation-name: translatetotopanim;
}

.solve {
  animation-duration: 2s;
  animation-fill-mode: forwards;
  animation-name: solveanim;
}

.dissolve {
  animation-duration: 1s;
  animation-fill-mode: forwards;
  animation-name: dissolveanim;
}

.title {
  left: 50%;
  top: 50%;
  position: absolute;
  transform: translate(-50%, -50%);
  font-size: 20vh;
}

#howg {
  margin-top: 24vh;
  margin-left: 5vh;
  font-size: 10vh;
}


#techg {
  margin-top: 24vh;
  margin-left: 5vh;
  font-size: 10vh;
}

#pecex {
  margin-top: 24vh;
  margin-left: 5vh;
  font-size: 10vh;
}
</style>