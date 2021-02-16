<template>
  <div style="
      position: absolute;
    top: 0;
    right: 5px;">
    <div id="chat" class="animated-chat tada" @click="loadChatbox">Chat</div>
    <div class="chatbox" id="chatbox">
      <span class="chat-text">Chatting!</span>
      <div
        id="smartchatbox_img901621879"
        style="
          width: 100%;
          height: 450px;
          overflow: hidden;
          margin: auto;
          padding: 0;
        "
      >
       
          <slot />
    
      </div>

      <div id="close-chat" @click="closeChatbox">&times;</div>
      <div id="minim-chat" @click="minimChatbox">
        <span class="minim-button">&minus;</span>
      </div>
      <div id="maxi-chat" @click="loadChatbox">
        <span class="maxi-button">&plus;</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    loadChatbox() {
      var e = document.getElementById("minim-chat");
      e.style.display = "block";
      var e = document.getElementById("maxi-chat");
      e.style.display = "none";
      var e = document.getElementById("chatbox");
      e.style.margin = "0";
    },
    closeChatbox() {
      var e = document.getElementById("chatbox");
      e.style.margin = "0 0 -1500px 0";
    },
    minimChatbox() {
      var e = document.getElementById("minim-chat");
      e.style.display = "none";
      var e = document.getElementById("maxi-chat");
      e.style.display = "block";
      var e = document.getElementById("chatbox");
      e.style.margin = "0 0 -460px 0";
    },
  },
};
</script>

<style scoped>
#chat,
#chat:after,
.chatbox {
  transition: all 0.4s ease-in-out;
}
#chat,
#close-chat,
.minim-button,
.maxi-button,
.chat-text {
  font-weight: 700;
  cursor: pointer;
  font-family: Arial, sans-serif;
  text-align: center;
 height: 25px;
    display: flex;
    line-height: 20px;
    align-items: center;
    justify-content: center;
    border-radius: 10px;
}
#chat,
#close-chat,
.chatbox {
  border: 1px solid #a8a8a8;
}
#chat:after,
#chat:before {
  position: absolute;
  border-style: solid;
  content: "";
}
.chatbox {
    max-width: 90%;
  position: fixed;
  bottom: 0;
  left: 20px;
  margin: 0 0 -1500px;
  background: #fff;
     /* border-bottom: none; */
    padding: 45px 0 0;
    z-index: 100000;
    border: 1px solid #e9e9e9;
    border-radius: 10px 10px 0 0;
    box-shadow: 1px 5px 15px #777474b5;
}
#close-chat {
  position: absolute;
  top: 8px;
  right: 5px;
  font-size: 24px;
  border: 1px solid #dedede;
  width: 20px;
  background: #fefefe;
  z-index: 2;
}
#minim-chat,
#maxi-chat {
  position: absolute;
  top: 6px;
  left: -5px;
  width: 100%;
  height: 20px;
  line-height: 20px;
  cursor: pointer;
  z-index: 1;
}
.minim-button {
  position: absolute;
  top: 2px;
  right: 26px;
  font-size: 24px;
  border: 1px solid #dedede;
  width: 20px;
  background: #fefefe;
}
.maxi-button {
  position: absolute;
  top: 2px;
  right: 26px;
  font-size: 24px;
  border: 1px solid #dedede;
  width: 20px;
  background: #fefefe;
}
.chat-text {
  position: absolute;
  top: 8px;
  left: 10px;
  font-size: 16px;
}
#chat {
  width: 60px;
  /* border-radius: 3px; */
  padding: 2px 8px;
  font-size: 16px;
  background: #611fc5 ;
  color: #fff;
  -webkit-transform: translateZ(0);
  transform: translateZ(0);
      position: absolute;
    top: 5px;
    right: 5px;
    border: 1px solid #0000003b;
}
#chat:before {
  border-width: 10px 11px 0 0;
  border-color: #611fc5  transparent transparent;
  left: 7px;
  bottom: -10px;
}
#chat:after {
  border-width: 9px 8px 0 0;
  border-color: #611fc5  transparent transparent;
  left: 8px;
  bottom: -8px;
}
#chat:hover {
  /* background: #ddd; */
  -webkit-animation-name: hvr-pulse-grow;
  animation-name: hvr-pulse-grow;
  -webkit-animation-duration: 0.3s;
  animation-duration: 0.3s;
  -webkit-animation-timing-function: linear;
  animation-timing-function: linear;
  -webkit-animation-iteration-count: infinite;
  animation-iteration-count: infinite;
  -webkit-animation-direction: alternate;
  animation-direction: alternate;
}
#chat:hover:after {
  border-color: #ddd transparent transparent !important;
}
.animated-chat {
  -webkit-animation-duration: 1s;
  animation-duration: 1s;
  -webkit-animation-fill-mode: both;
  animation-fill-mode: both;
  -webkit-animation-timing-function: ease-in;
  animation-timing-function: ease-in;
}
@-webkit-keyframes tada {
  0% {
    -webkit-transform: scale(1);
  }
  10%,
  20% {
    -webkit-transform: scale(0.9) rotate(-3deg);
  }
  30%,
  50%,
  70%,
  90% {
    -webkit-transform: scale(1.1) rotate(3deg);
  }
  40%,
  60%,
  80% {
    -webkit-transform: scale(1.1) rotate(-3deg);
  }
  100% {
    -webkit-transform: scale(1) rotate(0);
  }
}
@keyframes tada {
  0% {
    transform: scale(1);
  }
  10%,
  20% {
    transform: scale(0.9) rotate(-3deg);
  }
  30%,
  50%,
  70%,
  90% {
    transform: scale(1.1) rotate(3deg);
  }
  40%,
  60%,
  80% {
    transform: scale(1.1) rotate(-3deg);
  }
  100% {
    transform: scale(1) rotate(0);
  }
}
.tada {
  -webkit-animation-name: tada;
  animation-name: tada;
}
@-webkit-keyframes hvr-pulse-grow {
  to {
    -webkit-transform: scale(1.1);
    transform: scale(1.1);
  }
}
@keyframes hvr-pulse-grow {
  to {
    -webkit-transform: scale(1.1);
    transform: scale(1.1);
  }
}



</style>