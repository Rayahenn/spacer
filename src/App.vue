<template>
  <div :class="[{ flexStart: step === 1 }, 'wrapper']">
    <transition name="slide">
        <img src="./assets/logo.svg" class="logo" v-if="step === 1">
    </transition>
    <transition name="fade">
      <Heroimage v-if ="step === 0" />
    </transition>
    <Claim v-if ="step === 0" />
    <Searchinput :value="searchValue" v-model="searchValue" @input="handleInput" :dark="step === 1" />
    <div class="results" v-if="results && !loading && step === 1">
        <Item v-for="item in results" 
        :item="item" 
        :key="item.data[0].nasa_id" 
        @click.native="handleModalOpen(item)" />
      </div>
      <Modal v-if="modalOpen" :item="modalItem" @closeModal="modalOpen = false"/>
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim';
import Searchinput from '@/components/Searchinput';
import Heroimage from '@/components/Heroimage';
import Item from '@/components/Item';
import Modal from '@/components/Modal';

const API = 'https://images-api.nasa.gov';

export default {
  name: 'Search',
  components: {Claim, Searchinput, Heroimage, Item, Modal},
  data() {
    return {
      modalOpen: false,
      modalItem: null,
      loading: false,
      step: 0,
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function returnResponse() {
      this.loading = true;
      console.log(this.searchValue);
      axios.get(`${API}/search?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),

    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    }
  },
};
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800&display=swap');
  * {
    box-sizing: border-box;
  }

  body {
    font-family: Arial;
    margin: 0;
    padding: 0;
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s ease;
  }
  .fade-enter, .fade-leave-to {
    opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
    transition: opacity .3s ease;
  }
  .slide-enter, .slide-leave-to {
    margin-top: -50px;
  }

    .wrapper {
    display: flex;
    flex-direction: column;
    position: relative;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
    height: 100vh;
    justify-content: center;

    &.flexStart {
      justify-content: flex-start;
    }
  }

  .logo {
    position: absolute;
    top: 40px;
  }

  .results {
    margin-top: 50px;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;

    @media(min-width: 768px) {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }
</style>
