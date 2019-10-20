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
    height: 100px;
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
  <div class="results">
    
  </div>
</div>

</template>

<script>

import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from './components/Claim.vue';
import SearchInput from './components/SearchInput.vue';
import HeroImage from './components/HeroImage.vue';

const API = 'https://images-api.nasa.gov/search';

export default {
  name: 'App',

  components: {
    Claim,
    SearchInput,
    HeroImage,
  },

  data() {
    return {
      searchValue: '',
      results: [],
      step: 0,
      loading: false,
    };
  },
  methods: {
    handleInput: debounce(function () {
      this.loading = true;
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.loading = false;
          this.step = 1;
          this.results = response.data.collection.items;
          console.log(this.results);
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};

</script>
