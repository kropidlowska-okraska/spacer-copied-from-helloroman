<template>
  <div :class="[{flexStart: step === 1}, 'wrapper']">
    <transition name="slide ">
      <img src="../assets/spacer_logo.svg" alt="Logo" class="logo" v-if="step === 1" />
    </transition>
    <transition name="fade">
      <HeroImage v-if="step === 0"/>
    </transition>
    <Claim v-if="step === 0"/>
    <SearchInput v-model="searchValue" @input="handleInput" :dark="step === 1"/>
    <div class="results" v-if="results && !loading && step === 1 ">
      <Item
        v-for="item in results"
        :key="item.data[0].nasa_id"
        :item="item"
        @click.native="handleModalOpen(item)"
      />
    </div>
    <div class="loading"
         v-if="step === 1 && loading"
    ><div></div><div></div><div></div><div></div></div>
    <Modal
      v-if="modalOpen"
      :item="modalItem"
      @closeModal="modalOpen = false"
    />
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim.vue';
import SearchInput from '@/components/SearchInput.vue';
import HeroImage from '@/components/HeroImage.vue';
import Item from '@/components/Item.vue';
import Modal from '@/components/Modal.vue';

const API_NASA = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  components: {
    Modal,
    HeroImage,
    SearchInput,
    Claim,
    Item,
  },
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
    handleModalOpen(item) {
      this.modalOpen = true;
      this.modalItem = item;
    },

    handleInput: debounce(function () {
      this.loading = true;
      axios.get(`${API_NASA}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
          this.loading = false;
          this.step = 1;
        })
        .catch(error => console.error(error));
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
  .wrapper {
    position: relative;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    width: 100%;
    min-height: 100vh;
    margin: 0;
    padding: 30px;
  }

  .flexStart {
    justify-content: flex-start;
    padding: 0;
  }

  .logo {
    position: absolute;
    top: 30px;
    width: 100px;
  }

  .results {
    width: 80%;
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
    padding-top: 40px;

    @media (min-width: 768px) {
      grid-template-columns: 1fr 1fr 1fr;
    }
  }

  .fade-enter-active, .fade-leave-active {
    transition: opacity .3s ease;
  }
  .fade-enter, .fade-leave-to  {
    opacity: 0;
  }

  .slide-enter-active, .slide-leave-active {
    transition: margin-top  .3s ease;
  }
  .slide-enter, .slide-leave-to  {
    margin-top: -50px ;
  }

  .loading {
    display: inline-block;
    position: relative;
    width: 64px;
    height: 64px;
    margin-top: 60px;
  }
  .loading div {
    box-sizing: border-box;
    display: block;
    position: absolute;
    width: 51px;
    height: 51px;
    margin: 6px;
    border: 6px solid darkblue;
    border-radius: 50%;
    animation: loading 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
    border-color: darkblue transparent transparent transparent;
  }
  .loading div:nth-child(1) {
    animation-delay: -0.45s;
  }
  .loading div:nth-child(2) {
    animation-delay: -0.3s;
  }
  .loading div:nth-child(3) {
    animation-delay: -0.15s;
  }
  @keyframes loading {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
</style>
