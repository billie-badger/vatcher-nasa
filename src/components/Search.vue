<template>
  <div class="search">
    <h2>Vatcher NASA images</h2>
    <h3>What would you like NASA to show you?</h3>
    <form v-on:submit.prevent="getResult(query)">
      <input type="text" placeholder="Search NASA images..." v-model="query" />
    </form>
    <div class="results" v-if="results">
      <div v-for="result in results">
        <img v-bind:src="result.links[0].href"  />
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'search',
  data () {
    return {
      msg: 'Search',
      query: '',
      results: ''
    }
  },
  methods: {
    getResult(query){
      axios.get('https://images-api.nasa.gov/search?q=' + query + '&media_type=image').then( response => {
        console.log(response.data.collection.items);
        this.results = response.data.collection.items;
      });
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.results img{
  width: 50%;
  margin: 15px auto;
}
h1, h2 {
  color: #ededed;
  font-weight: normal;
}
h3{
  color: gray;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

input{
  padding: 10px;
  border-radius: 5px;
  border: 1px solid #ededed;
  color: #ededed;
  background: #272727;
}
</style>
