<template>
  <div class="chat-container" id="chat-component">
      <div v-for="(message, index) in messages" 
      :key="index" 
      class="message-container" 
      v-bind:class="{'from-user' : (message.from == member.name) || (message.from == 'user')}">
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
        memberString: {
            type: String,
            required: true,
        },
        unreadCount: {
            type: Number,
            required: true,
        },
        incrementUnreadCount: {
            type: Function, 
            required: false,
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
                  from: 'user',
                  text: 'hello!',
              },
              {
                  from: 'user',
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
                  from: 'user',
                  text: 'nice okay!',
              },
              {
                  from: 'user',
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
          if (this.incrementUnreadCount) this.incrementUnreadCount();
        //   this.unreadCount += 1; // causes error, doesn't increment;
          this.$emit('increment');


        var event = document.createEvent("HTMLEvents");
        event.initEvent("increment", true, true);
        event.eventName = "increment";
        var element = document.getElementById('chat-component')
        element.dispatchEvent(event);
      }
  },
  computed: {
    member() {
        console.log('this.memberString = ', this.memberString);
        if (this.memberString) {
            return JSON.parse(this.memberString)
        } else {
            return {}
        }
    }
  },
  mounted() {
      console.log('hello world we are mounted');
  }
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
