<template>
  <div>
    <div class="hello">
      <h1>{{ msg }}</h1>
    </div>
    <div>
      Enter full url! <input type="text" v-model="fullUrl">
    </div>
    <div>
      <button v-on:click="getShortUrl()"> Convert! </button>
      <p> Shortened url: {{shortUrl}} </p>
    </div>
    <div>
      Enter shortened url! <input type="text" v-model="shortUrl">
    </div>
    <div>
      <button v-on:click="goToUrl()"> Go! </button>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'hello',
  data () {
    return {
      msg: 'URL Shortening Service',
      fullUrl: '',
      shortUrl: ''
    }
  },
  methods: {
    getShortUrl: function () {
      axios.post('http://localhost:8081/api/short', {full_url: this.fullUrl})
      .then(response => {
        this.shortUrl = response.data['url']
      })
    },
    goToUrl: function () {
      axios.post('http://localhost:8081/api/full', {short_url: this.shortUrl})
      .then(response => {
        console.log(response)
        this.fullUrl = response.data['url']
        window.location.href = 'http://' + this.fullUrl
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
</style>
