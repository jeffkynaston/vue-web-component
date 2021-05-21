<template>
  <div class="home">
    <!-- <h1>this is an parent page that holds chat</h1>
    <div class="unread-count">unread count (passed handler to increment): {{otherUnreadCount}}</div>
    <div class="unread-count">unread count (passed via integer) {{unreadCount}}</div>
    <div class="unread-count">unread count (passed via emit) {{emitCount}}</div> -->
    <div class="parent-chat-wrapper">
      <Chat :member="member" 
            :unreadCount="unreadCount" 
            v-on:increment="incrementEmitCount"
            :incrementUnreadCount="incrementUnreadCount"/>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
import Chat from '@/components/Chat.vue'

export default {
  name: 'Home',
  components: {
    Chat
  },
  data: function() {
    return {
      member: "{name: 'kevin'}",
      unreadCount: 0,
      emitCount: 0,
      otherUnreadCount: 0,
    }
  },
  methods: {
    incrementUnreadCount() {
      this.otherUnreadCount += 1;
    },
    incrementEmitCount() {
      console.log('incrementEmitCount fired!!');
      this.emitCount += 1;
    }
  }
}
</script>

<style scoped>
  .parent-chat-wrapper {
    width: 400px;
    height: 600px;
    margin: auto;
    position: relative;
  }
  .unread-count {
    text-align: left;
    width: 400px;
    margin: auto;
  }
</style>