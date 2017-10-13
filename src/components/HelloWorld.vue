<template>
  <div>
    <div class="hello">
      <h1>{{ msg }}</h1>
    </div>
    <div>
      Enter full url! <input type="text" v-model="fullUrl">
    </div>
    <div>
      <button v-on:click="convertUrl()"> Convert! </button>
      <p> Shortened url: {{userAgent}} </p>
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
      shortUrl: '',
      userAgent: ''
    }
  },
  methods: {
    convertUrl: function () {
      axios.get('https://api.github.com/users/codeheaven-io')
      .then(response => {
        this.userAgent = response.data['login']
      })
    },
    goToUrl: function () {
      // Backend todo : prepend http to output
      window.location.href = 'http://naver.com'
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
