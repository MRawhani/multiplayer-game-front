<template>
  <div class="members task-box "
  :style="{background:`${msg.color}36`}"
  >
     <img
            :src="`http://i.pravatar.cc/500?img=${msg.from||7}`"
            alt="member">
  <div class="message">
      
    <div class="message__title">
      <h4> {{ msg.from }}</h4>
      <span>
        {{ msg.createAt | formatTime }}
      </span>
    </div>
    <div class="message__body">
      <p v-if="msg.text">{{ msg.text }}</p>
      <p v-else>
        <a :href="msg.url" target="_blank">My location</a>
      </p>
    </div>

  </div>
  </div>
</template>

<script>
import { format } from 'date-fns'
export default {
  name: 'chat-message',
  props: {
    msg: {
      type: Object,
      required: true,
    },
  },
  filters: {
    formatTime(str) {
      return format(str, 'HH:mm a')
    },
  },
}
</script>

<style>
</style>
