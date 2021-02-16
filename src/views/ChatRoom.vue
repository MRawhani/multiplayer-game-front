<template>
  <div class="">
    <div class="task-manager">
  <div class="left-bar">
    <div class="upper-part">
      <div class="actions">
        <div class="circle"></div>
        <div class="circle-2"></div>
      </div>
    </div>
    <div class="left-content">
      <!-- <ul class="action-list">
        <li class="item">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="currentColor"
            stroke-linecap="round" stroke-linejoin="round" stroke-width="2" class="feather feather-inbox"
            viewBox="0 0 24 24">
            <path d="M22 12h-6l-2 3h-4l-2-3H2" />
            <path
              d="M5.45 5.11L2 12v6a2 2 0 0 0 2 2h16a2 2 0 0 0 2-2v-6l-3.45-6.89A2 2 0 0 0 16.76 4H7.24a2 2 0 0 0-1.79 1.11z" />
          </svg>
          <span>Inbox</span>
        </li>
        <li class="item">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
            class="feather feather-star">
            <polygon
              points="12 2 15.09 8.26 22 9.27 17 14.14 18.18 21.02 12 17.77 5.82 21.02 7 14.14 2 9.27 8.91 8.26 12 2" />
            </svg>
          <span> Today</span>
        </li>
        <li class="item">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="currentColor"
            stroke-linecap="round" stroke-linejoin="round" stroke-width="2" class="feather feather-calendar"
            viewBox="0 0 24 24">
            <rect width="18" height="18" x="3" y="4" rx="2" ry="2" />
            <path d="M16 2v4M8 2v4m-5 4h18" />
          </svg>
          <span>Upcoming</span>
        </li>
        <li class="item">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
            class="feather feather-hash">
            <line x1="4" y1="9" x2="20" y2="9" />
            <line x1="4" y1="15" x2="20" y2="15" />
            <line x1="10" y1="3" x2="8" y2="21" />
            <line x1="16" y1="3" x2="14" y2="21" /></svg>
          <span>Important</span>
        </li>
        <li class="item">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
            stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
            class="feather feather-users">
            <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2" />
            <circle cx="9" cy="7" r="4" />
            <path d="M23 21v-2a4 4 0 0 0-3-3.87" />
            <path d="M16 3.13a4 4 0 0 1 0 7.75" /></svg>
          <span>Meetings</span>
        </li>
        <li class="item">
          <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" stroke="currentColor"
            stroke-linecap="round" stroke-linejoin="round" stroke-width="2" class="feather feather-trash"
            viewBox="0 0 24 24">
            <path d="M3 6h18m-2 0v14a2 2 0 0 1-2 2H7a2 2 0 0 1-2-2V6m3 0V4a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v2" />
          </svg>
          <span>Trash</span>
        </li>
      </ul> -->
    
    </div>
  </div>
  <div class="page-content">
    <div class="header">Win it</div>
      <game />
  
  </div>
  <div class="right-bar">
    <div class="top-part">
       <div style="display:flex; margin:0 10px; padding:10px" >
            <user-avatar v-for="user in users" :key="user.name" :avatar="user" :active="active"/>
          </div>
      <!-- <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none"
        stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round"
        class="feather feather-users">
        <path d="M17 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2" />
        <circle cx="9" cy="7" r="4" />
        <path d="M23 21v-2a4 4 0 0 0-3-3.87" />
        <path d="M16 3.13a4 4 0 0 1 0 7.75" /></svg> -->
      <div class="count">{{users.length || 0}}</div>
    </div>
    <div class="header">Chatting</div>
    <div class="right-content">
      <section class="chat__main">
      <ol class="chat__messages">
        <chat-message v-for="msg in messages" :msg="msg" :key="msg.createAt"></chat-message>
      </ol>

  
    </section>
    
    </div>
        <footer class="chat__footer">

        <form @submit.prevent="sendMessage">
          <input type="text" placeholder="Message" required v-model="message" autofocus autocomplete="off" />

          <button type="submit">Send</button>
        </form>

        <!-- <button :disabled="isButtonDisabled" @click="startAudioChat">Audio Chat</button> -->

      </footer>
  </div>
</div>
<!-- <chat-box >

 
</chat-box>
  -->
    <!-- <aside class="chat__sidebar">
      <h3 v-if="loading">loading</h3>
      <h3 v-else>people</h3>
      <div id="users">
        <ol>
          <li v-for="user in users" :key="user">
            <user-avatar :avatar="user"/>
          </li>
        </ol>
      </div>
    </aside> -->

    <!-- <section class="chat__main">
      <ol class="chat__messages">
        <chat-message v-for="msg in messages" :msg="msg" :key="msg.createAt"></chat-message>
      </ol>

      <footer class="chat__footer">

        <form @submit.prevent="sendMessage">
          <input type="text" placeholder="Message" required v-model="message" autofocus autocomplete="off" />

          <button type="submit">Send</button>
        </form>

        <button :disabled="isButtonDisabled" @click="startAudioChat">Audio Chat</button>

      </footer>
    </section> -->
    <v-dialog/>
    <audio id="audio-tag" autoplay playsinline></audio>
  </div>
</template>

<script>
import SimplePeer from 'simple-peer'

import ChatMessage from '@/components/ChatMessage'
import Game from '@/components/Game'
import ChatBox from '../components/ChatBox.vue'
import UserAvatar from '../components/UserAvatar.vue'
export default {
  name: 'chat-room',
  props: {
    name: {
      type: String,
      default: 'Henry',
    },
    room: {
      type: String,
      default: 'A',
    },
  },
  data() {
    return {
      message: '',
      colorString:'#000',
      loading:false,
      active:false,
      messages: [],
      isButtonDisabled: false,
      users: ['Henry', 'David'],
      peer: null,
      myAudioStream: null,
    }
  },
  sockets: {
    shareAudioModal(name) {
      // this.$modal.show('dialog', {
      //   title: 'Start Audio Conversation',
      //   text: name + 'would like to start an audio chat with you.',
      //   buttons: [
      //     {
      //       title: 'Accept', // Button title
      //       default: true, // Will be triggered by default if 'Enter' pressed.
      //       handler: this.acceptAudioChat, // Button click handler
      //     },
      //     {
      //       title: 'Refuse',
      //     },
      //   ],
      // })
      this.acceptAudioChat()
    },
    updateUserList(users) {
      this.users = users
    },
      active(a) {
      this.active = a
    
    },
    newMessage(msg) {
      console.log(msg)
      this.messages.push(msg)
    },
    transmitOffer(data) {
      console.log('receiving Offer', data)
      if (this.peer === null) {
        // peer 2
        this.peer = new SimplePeer({
          initiator: false,
          stream: this.myAudioStream,
          config: {
            iceServers: [
              {
                urls: 'stun:stun.l.google.com:19302',
              },
              {
                urls: 'stun:global.stun.twilio.com:3478?transport=udp',
              },
              {
                urls: 'turn:numb.viagenie.ca',
                credential: 'hiragana',
                username: 'mornirmornir@hotmail.com',
              },
            ],
          },
        })
        this.bindEvents(this.peer)
      }
debugger
      this.peer.signal(data)
    },
  },
  methods: {
    async acceptAudioChat() {
      console.log('YES!!')
      this.$modal.hide('dialog')
      this.loading = true
      try {
        const stream = await navigator.mediaDevices.getUserMedia({
          video: false,
          audio: true,
        })
        this.peer = new SimplePeer({
          initiator: true,
          stream,
          config: {
            iceServers: [
              { urls: 'stun:stun.l.google.com:19302' },
              { urls: 'stun:global.stun.twilio.com:3478?transport=udp' },
              {
                urls: 'turn:numb.viagenie.ca',
                credential: 'hiragana',
                username: 'mornirmornir@hotmail.com',
              },
            ],
          },
        })
        this.isButtonDisabled = true;
      this.loading = false
        
        this.bindEvents(this.peer)
      } catch (e) {
        console.log(e.message)
      this.loading = false

      }
    },
    async startAudioChat() {
      try {
        this.myAudioStream = await navigator.mediaDevices.getUserMedia({
          video: false,
          audio: true,
        })
        this.$socket.emit('askAudio')

      } catch (e) {
        console.log(e.message)

      }
    },
    sendMessage() {
      this.$socket.emit('createMessage', { text: this.message }, () => {
        this.message = ''
      })
    },
    bindEvents(p) {
      p.on('error', err => {
        console.log(err)
      })

      p.on('signal', data => {
        this.$socket.emit('createOffer', data)
      })

      p.on('stream', stream => {
        console.log('got remote audio stream', stream)
        document.querySelector('#audio-tag').srcObject = stream
      })
    },
  },
  mounted(){
var myAudio = document.querySelector('#audio-tag');
myAudio.onplaying = function() {
    // alert("The audio is now playing");
};
myAudio.onpause = function() {
   // alert("The audio is now paused");
};
// if (myAudio.duration > 0 && !myAudio.paused) {

//     //Its playing...do your job

// } else {

//     //Not playing...maybe paused, stopped or never played.

  // }
  },
  created() {
    this.$socket.emit('join', { name: this.name, room: this.room }, err => {
      if (err) {
        alert(err)
      } else {
        console.log('No error')
        this.startAudioChat()
      }
    })
  },
  components: {
    ChatMessage,
    Game,
    ChatBox,
    UserAvatar,
  },
}
</script>

<style>
</style>
