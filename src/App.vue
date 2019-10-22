<style lang="scss">

@import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,700&display=swap');
* {
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  -mos-osx-font-smoothing: grayscale;
}

body {
  margin: 0;
  padding: 0;
  font-family: "Montserrot", sans-serif;
}

.fade-enter-active, .fade-leave-active {
  transition: opacity .6s ease;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
}

.slide-enter-active, .slide-leave-active {
  transition: margin-top .4s ease;
}

.slide-enter, .slide-leave-to {
  margin-top: -10;
}

.wrapper {
  margin: 0;
  width: 100%;
  min-height: 100vh;
  padding: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  position: relative;

  &.upper {
    justify-content: flex-start;
  }

  .logo {
    position: absolute;
    top: 30px;
    left: 30px;
    height: 100px;

    @media (max-width: 768px) {
      top: 30px;
      height: 20px;
    }
  }

  .results {
    margin-top: 50px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;

    @media (min-width: 768px) {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }

  .lds-ellipsis {
    display: inline-block;
    position: relative;
    width: 64px;
    height: 64px;

    @media(min-width: 768px) {
      width: 90px;
      height: 90px;
    }
  }
  .lds-ellipsis div {
    position: absolute;
    top: 127px;
    width: 11px;
    height: 11px;
    border-radius: 50%;
    background: #333;
    animation-timing-function: cubic-bezier(0, 1, 1, 0);
  }
  .lds-ellipsis div:nth-child(1) {
    left: 6px;
    animation: lds-ellipsis1 0.6s infinite;
  }
  .lds-ellipsis div:nth-child(2) {
    left: 6px;
    animation: lds-ellipsis2 0.6s infinite;
  }
  .lds-ellipsis div:nth-child(3) {
    left: 26px;
    animation: lds-ellipsis2 0.6s infinite;
  }
  .lds-ellipsis div:nth-child(4) {
    left: 45px;
    animation: lds-ellipsis3 0.6s infinite;
  }
  @keyframes lds-ellipsis1 {
    0% {
      transform: scale(0);
    }
    100% {
      transform: scale(1);
    }
  }
  @keyframes lds-ellipsis3 {
    0% {
      transform: scale(1);
    }
    100% {
      transform: scale(0);
    }
  }
  @keyframes lds-ellipsis2 {
    0% {
      transform: translate(0, 0);
    }
    100% {
      transform: translate(19px, 0);
    }
  }
}

</style>

<template>

<div id="app" :class="[{upper: step === 1}, 'wrapper']">
  <transition name="slide">
    <img src="./assets/logo.png" class="logo" v-if="step === 1">
  </transition>
  <Claim v-if="step === 0"/>
  <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
  <transition name="fade">
    <HeroImage v-if="step === 0" />
  </transition>
  <div class="results" v-if="results && !loading && step === 1">
    <Item v-for="item in results" :item="item" :key="item.data[0].nasa_id" @click.native="handleModal(item)"/>
  </div>
  <div class="lds-ellipsis" v-if="step === 1 && loading"><div></div><div></div><div></div><div></div></div>
  <Modal v-if="modal" @closeModal="modal=false" :item="modalItem"/>
</div>

</template>

<script>

import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from './components/Claim.vue';
import SearchInput from './components/SearchInput.vue';
import HeroImage from './components/HeroImage.vue';
import Item from './components/Item.vue';
import Modal from './components/Modal.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'App',

  components: {
    Claim,
    SearchInput,
    HeroImage,
    Item,
    Modal,
  },

  data() {
    return {
      modal: false,
      modalItem: null,
      searchValue: '',
      results: [],
      step: 0,
      loading: false,
    };
  },
  methods: {
    handleModal(item) {
      this.modalItem = item;
      this.modal = true;
    },
    handleInput: debounce(function () {
      this.loading = true;
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.loading = false;
          this.step = 1;
          this.results = response.data.collection.items;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};

</script>
