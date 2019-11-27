<template>
  <div class="leftPane">
    <div class="brandInfo">
      <img class="brandLogo" :src="BRAND_LOGO" resize="contain" />
      <span class="brandName">{{BRAND_NAME}}</span>
    </div>
    <div class="searchBox">
      <img class="searchIcon" :src="SEARCH_ICON" resize="contain" />
      <input class="searchInput" v-model="searchText" placeholder="Search Messenger" />
    </div>
    <ul class="receiversList">
      <li
        v-for="(receiver, index) in messagesMap"
        :key="`receiver_${index}`"
        :class="[index === selectedReceiver && 'activeReceiver']"
      >
        <ReceiverComponent
          :lastMessage="receiver[receiver.length - 1]"
          :selectReceiver="selectReceiver"
          :index="index"
          :isSelected="index === selectedReceiver"
        />
      </li>
    </ul>
  </div>
</template>

<script>
  import ReceiverComponent from './ReceiverComponent.vue';
  import { BRAND_NAME } from '../../../constants';
  import { BRAND_LOGO, SEARCH_ICON } from '../../../images';

  export default {
    components: {
      ReceiverComponent,
    },
    props: {
      messages: Array,
      messagesMap: Object,
      selectedReceiver: String,
      selectReceiver: {
        type: Function,
        default: () => {},
      },
    },
    data: () => ({
      BRAND_NAME,
      BRAND_LOGO,
      SEARCH_ICON,
      searchText: '',
    }),
    methods: {
    },
    created() {
      
    },
  };
</script>

<style scoped lang="scss">
  @import '../../../commonStyles/index.scss';

  .leftPane {
    display: flex;
    flex: 0.3;
    height: 100vh;
    flex-direction: column;
    background-color: $Whisper;
  }

  .brandInfo {
    display: flex;
    height: 100px;
    align-items: center;
    background-color: $White;
  }

  .brandLogo {
    @include margin(30px, 20px);
    @include width(40px, 40px);
  }

  .brandName {
    @include font-style(26px, $Charcoal, 600);
  }

  .searchBox {
    display: flex;
    height: 40px;
    background-color: $White;
  }

  .searchIcon {
    @include width(40px, 40px);
    @include margin(0, 20px);
  }

  .searchInput {
    display: flex;
    flex: 1;
    height: 40px;

    @include font-style(18px, $Charcoal);
  }

  .receiversList {
    display: flex;
    flex: 1;
    background-color: $White;
    flex-direction: column;
    overflow: scroll;
  }

  .activeReceiver {
    background-color: $Whisper; 
  }

</style>
