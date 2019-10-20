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

.wrapper {
  margin: 0;
  width: 100%;
  min-height: 100vh;
  padding: 30px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

</style>

<template>

<div id="app" class="wrapper">
    <Claim />
    <SearchInput v-model="searchValue" @input="handleInput" />
    <HeroImage />
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
    };
  },
  methods: {
    handleInput: debounce(function () {
      console.log(this.searchValue);
      axios.get(`${API}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
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
