<template>
  <div class="receiverContainer" @click="chooseReceiver">
    <div class="lastMessageContainer">
      <span :class="['receiverImage', isSelected && 'selectedImage']"></span>
      <div class="receiverBox">
        <span class="receiverName">{{lastMessageReceiver}}</span>
        <span class="lastMessage">{{lastMessage.sender_name === USERNAME ? 'You: ' : ''}}{{lastMessage.content}}</span>
      </div>
      <span class="messageTime">{{getTime}}</span>
    </div>
  </div>
</template>

<script>
  import { USERNAME } from '../../../constants';

  export default {
    props: {
      lastMessage: Object,
      index: String,
      isSelected: Boolean,
      selectReceiver: {
        type: Function,
        default: () => {},
      }
    },
    data: () => ({
      USERNAME,
    }),
    computed: {
      getTime() {
        // const currentDate = new Date();
        const messagedDate = new Date(this.lastMessage.message_at);
        const hours = messagedDate.getHours();
        let minutes = messagedDate.getMinutes();
        minutes = minutes / 10 >= 1 ? minutes : `0${minutes}`;
        return `${hours}:${minutes}`;
      },
      lastMessageReceiver() {
        return this.lastMessage.receiver_name !== USERNAME ? this.lastMessage.receiver_name : this.lastMessage.sender_name;
      },
    },
    methods: {
      chooseReceiver() {
        this.selectReceiver(this.index);
      },
    },
    created() {

    },
  };
</script>

<style scoped lang="scss">
  @import '../../../commonStyles/index.scss';

  .receiverContainer {
    display: flex;
    flex: 1;
    height: 100px;
    align-items: center;
  }

  .receiverImage {
    border-radius: 20px;
    background-color: $Whisper;

    @include width(40px, 40px);
    @include margin(0, 20px);
  }

  .selectedImage {
    background-color: $White;
  }

  .lastMessageContainer {
    display: flex;
  }

  .receiverBox {
    display: flex;
    flex: 1;
    flex-direction: column;
  }

  .receiverName {
    width: 200px;
    text-align: left;

    @include ellipsis();
  }
  
  .messageTime {
    margin-right: 10px;
  }

  .lastMessage {
    width: 200px;
    text-align: left;

    @include ellipsis();
  }

</style>
