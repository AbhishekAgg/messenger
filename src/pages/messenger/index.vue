<template>
  <div class="messengerWindow">
    <LeftPane
      :messages="messages"
      :messagesMap="groupByReceivers"
      :selectedReceiver="selectedReceiver"
      :selectReceiver="selectReceiver"
    />
    <RightPane :messages="selectedMessages" :selectedReceiver="selectedReceiver" />
  </div>
</template>

<script>
  // Import all components here
  import LeftPane from './components/LeftPane.vue';
  import RightPane from './components/RightPane.vue';
  // Import all constants and helper methods here
  import { USERNAME } from '../../constants';
  // import { messageEndpoint } from '../../urls';

  export default {
    components: {
      LeftPane,
      RightPane,
    },
    data: () => ({
      messages: [],
      selectedReceiver: '',
      selectedMessages: [],
    }),
    computed: {
      groupByReceivers() {
        let messagesMap = {};
        this.messages.forEach((message) => {
          const receiver = message.receiver_name;
          const sender = message.sender_name;
          if (messagesMap[receiver] !== USERNAME) {
            if (!messagesMap[receiver]) {
              messagesMap[receiver] = [];
            }
            messagesMap[receiver].push(message);
          } else if (messagesMap[sender] !== USERNAME) {
            if (!messagesMap[sender]) {
              messagesMap[sender] = [];
            }
            messagesMap[sender].push(message);
          }
        });
        if (!this.selectedReceiver) {
          // eslint-disable-next-line
          this.selectedReceiver = Object.keys(messagesMap)[0] || '';
          // eslint-disable-next-line
          this.selectedMessages = messagesMap[this.selectedReceiver];
        }
        return messagesMap;
      },
    },
    methods: {
      fetchMessages() {
        fetch('http://demo5942710.mockable.io/messages', {
          method: 'GET',
        }).then(response => {
          if (response.ok) {
            response.json().then(json => {
              this.messages = json;
            });
          }
        });
      },
      selectReceiver(receiver) {
        // debugger;
        this.selectedReceiver = receiver;
        this.selectedMessages = this.groupByReceivers[receiver];
      },
      updateMessage(operation, message, index) {
        if (operation === 'ADD') {
          this.messages.push(message);
        } else if (operation === 'DELETE') {
          this.messages.splice(index, 1);
        }
      },
    },
    created() {
      this.fetchMessages();
    },
  };
</script>

<style scoped lang="scss">
  @import '../../commonStyles/index.scss';

  .messengerWindow {
    display: flex;
    flex: 1;
  }
  
</style>
