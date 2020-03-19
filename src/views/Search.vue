<template>
  <div class="wrapper">
    <Claim />
    <Searchinput />
  </div>
</template>

<script>
import axios from 'axios';
import debounce from 'lodash.debounce';
import Claim from '@/components/Claim';
import Searchinput from '@/components/Searchinput';

const API = 'https://images-api.nasa.gov';

export default {
  name: 'Search',
  components: {Claim, Searchinput},
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function returnResponse() {
      axios.get(`${API}/search?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
        })
        .catch((error) => {
          console.log(error);
        });
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin: 0;
    padding: 30px;
    width: 100%;
    height: 100vh;
    justify-content: center;
    background-image: url('../assets/heroimage.jpg');
    background-repeat: no-repeat;
    background-size: cover;
    background-position: 30% 0%;
  }

</style>
