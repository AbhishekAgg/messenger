<template>
  <div class="rightPane">
    <div class="receiverHeader">
      <span class="receiverName">{{selectedReceiver}}</span>
      <span>Active on Facebook</span>
    </div>
    <div>
      <!-- TODO - Add messages corresponding to selected Receiver -->
      <!-- <ul class="messagesContainer">
        <li v-for="(message, index) in messages" :key="`message_${index}`">

        </li>
      </ul> -->
    </div>
  </div>
</template>

<script>

  export default {
    props: {
      messages: Array,
      selectedReceiver: String,
    },
    data: () => ({
    }),
    methods: {
      
    },
  };
</script>

<style scoped lang="scss">
  @import '../../../commonStyles/index.scss';

  .rightPane {
    display: flex;
    flex: 0.7;
    flex-direction: column;
    background-color: $Whisper;
  }

  .receiverHeader {
    display: flex;
    height: 100px;
    flex-direction: column;
    background-color: $White;

    @include align(center, center);
  }

  .receiverName {
    font-weight: 700;
  }

  .messagesContainer {
    display: flex;
    flex-direction: column;
    flex: 1;
  }
  
</style>
