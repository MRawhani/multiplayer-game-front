<template>
  <div class="centered-form">
<inp-enter />
	<div class="input-wrap">
			<svg 
				class="cloudy"
				viewBox="0 0 277 145"
			>
				<path 
					class="cloudy-poofs"
					d="M218,20c-0.74,0-1.47,0.03-2.2,0.06C204.99,7.77,189.16,0,171.5,0c-12.22,0-23.58,3.72-33,10.09 C129.08,3.72,117.72,0,105.5,0C87.84,0,72.01,7.77,61.2,20.06C60.47,20.03,59.74,20,59,20C26.42,20,0,46.42,0,79 c0,32.58,26.42,59,59,59c5.26,0,10.36-0.7,15.21-1.99C83.28,141.7,94,145,105.5,145c12.22,0,23.58-3.72,33-10.09 c9.42,6.37,20.78,10.09,33,10.09c11.5,0,22.22-3.3,31.29-8.99c4.85,1.29,9.95,1.99,15.21,1.99c32.58,0,59-26.42,59-59 C277,46.42,250.58,20,218,20z"
				/>
			</svg>
		  <!-- <div class="form-field">
          <h3>Join</h3>
        </div> -->
			<div 
				:class="{ disabled: false }"
				class="dreamy-input"
			>
				<label 
					class="dreamy-input-label"
					for="dreamyInput"
				>name</label>
				<input 
					id="dreamyInput"
				v-model="name"
					:aria-describedby="false ? 'dreamyInputErr' : null"
					:disabled="false"
					autocomplete="off"
					class="dreamy-input-control"
					type="name"
			
				>
			
			</div>
      	<div 
				:class="{ disabled: false }"
				class="dreamy-input"
			>
				<label 
					class="dreamy-input-label"
					for="dreamyInput"
				>Choose Game</label>
				<input 
					id="dreamyInput"
				v-model="room"
					:aria-describedby="false ? 'dreamyInputErr' : null"
					:disabled="false"
					autocomplete="off"
					class="dreamy-input-control"
					type="text"
					@keydown.enter="goToRoom"
				>
			
			</div>
        <div class="form-field">
          <button 
					@click="goToRoom"
           type="submit" :disabled="disableButton">JOIN</button>
        </div>
		</div>
    <!-- <div class="centered-form__form">
      <form @submit.prevent="goToRoom">
        <div class="form-field">
          <h3>Join a Chat</h3>
        </div>
        <div class="form-field">
          <label for="name">Display name</label>
          <input type="text" name="name" autofocus required v-model="name">
        </div>
        <div class="form-field">
          <label for="room">Room name</label>
          <input type="text" name="room" required v-model="room">
        </div>
        <div class="error-message" v-if="err">{{ err }}</div>
        <div class="form-field">
          <button type="submit" :disabled="disableButton">JOIN</button>
        </div>
      </form>
    </div> -->
  </div>
</template>

<script>
import InpEnter from '../components/InpEnter.vue'
export default {
  components: { InpEnter },
  name: 'home',
  data() {
    return {
      name: '',
      room: '',
      err: null,
      disableButton: !this.$socket.connected,
    }
  },
  sockets: {
    // prevent joining if server is not up and running
    // in main.js linking socket.io to vue-sockets triggers the connect hook immediately on the first page displayed.
    connect_error(err) {
      console.error(err)
      this.disableButto = true
      this.err = `Cannot connect to server: ${err.message}`
    },
    connect() {
      console.log('connect')
      this.disableButton = false
    },
    reconnect() {
      console.log('reconnect')
      this.disableButton = false
    },
  },
  methods: {
    goToRoom() {
      this.$router.push(`/chat-room/${this.room}/${this.name}`)
    },
  },
}
</script>

<style scoped>
.error-message {
  color: #ff4136;
}
</style>

