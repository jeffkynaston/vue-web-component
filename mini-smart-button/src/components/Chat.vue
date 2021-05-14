<template>
  <div class="chat-container">
      <div v-for="(message, index) in messages" 
      :key="index" 
      class="message-container" 
      v-bind:class="{'from-user' : message.from == member.name}">
          <div class="message-from">{{message.from}}</div>
          <div class="message-text">{{message.text}}</div>
      </div>
      <button @click="addChat" class="add-chat">add chat</button>
  </div>
</template>

<script>
export default {
  name: 'Chat',
  props: {
            member: {
                type: Object,
                required: true,
            },
            unreadCount: {
                type: Number,
                required: true,
            },
            incrementUnreadCount: {
                type: Function, 
                required: true,
            }
    },
  data: function() {
      return {
          messages: [
              {
                  from: 'bot',
                  text: 'hello',
              },
              {
                  from: this.member.name,
                  text: 'hello!',
              },
              {
                  from: this.member.name,
                  text: 'I need help!',
              },
              {
                  from: 'bot',
                  text: 'I can maybe help',
              },
              {
                  from: 'bot',
                  text: 'no promises..',
              },  
              {
                  from: this.member.name,
                  text: 'nice okay!',
              },
              {
                  from: this.member.name,
                  text: 'thanks for trying',
              },            
              {
                  from: 'bot',
                  text: 'try restarting your computer',
              },
              {
                  from: 'bot',
                  text: 'that normally fixes it',
              },  
          ]
      }
  },
  methods: {
      addChat() {
          this.messages.push({
              from: this.member.name,
              text: 'new chat!',
          });
          this.incrementUnreadCount();
        //   this.unreadCount += 1; // causes error, doesn't increment;
          this.$emit('incrementChat');
      }
  },
}
</script>

<style scoped>
.chat-container {
    border: 1px solid lightslategray;
    padding: 12px;
    overflow: auto;
    position: absolute;
    top: 0px;
    bottom: 0px;
    left: 0px;
    right: 0px;
}

.message-container {
    text-align: left;
    margin-top: 12px;
}
.message-from {
    font-size: 12px;
    font-weight: bold;    
}
.message-text {
    font-size: 16px;
}
.from-user {
    text-align: right;
}
</style>
