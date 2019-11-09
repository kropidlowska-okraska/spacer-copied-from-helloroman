<template>
  <div class="wrapper">
    <div class="search">
      <label for="search">Search</label>
      <input
        type="text"
        name="search"
        id="search"
        v-model="searchValue"
        @input="handleInput"
       />
    </div>
    <ul>
      <li v-for="result in results" :key="result.data[0].nasa_id">
        {{ result.data[0] }}
      </li>
    </ul>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from 'axios';
import debounce from 'lodash.debounce';

const API_NASA = 'https://images-api.nasa.gov/search';

export default {
  name: 'Search',
  data() {
    return {
      searchValue: '',
      results: [],
    };
  },
  methods: {
    handleInput: debounce(function () {
      axios.get(`${API_NASA}?q=${this.searchValue}&media_type=image`)
        .then((response) => {
          this.results = response.data.collection.items;
        })
        .catch(error => console.log(error));
    }, 500),
  },
};
</script>

<style lang="scss" scoped>
  .wrapper {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 100%;
    margin: 0;
    padding: 30px;
  }

  .search {
    display: flex;
    flex-direction: column;
    align-items: center;
    width: 250px;

    label {
      font-family: Montserrat, sans-serif;
    }

    input {
      height: 30px;
      border: 0;
      border-bottom: 1px solid black;
    }
  }
</style>
