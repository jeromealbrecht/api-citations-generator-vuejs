<template>
  <div id="app">
    <h1>Générateur de Citations</h1>
    <button v-on:click="generateQuote">Générer une citation</button>
    <p>{{ quote }}</p>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      quote: '',
    }
  },
  methods: {
    generateQuote() {
      axios.get('https://type.fit/api/quotes')
        .then(response => {
          const quotes = response.data;
          const randomQuote = quotes[Math.floor(Math.random() * quotes.length)];
          this.quote = `${randomQuote.text} - ${randomQuote.author}`;
        })
        .catch(error => {
          console.error(error);
        });
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

button {
  background-color: #42b983;
  border: none;
  border-radius: 4px;
  color: #fff;
  cursor: pointer;
  font-size: 16px;
  margin-top: 20px;
  padding: 10px 20px;
  user-select: none;
}
</style>
