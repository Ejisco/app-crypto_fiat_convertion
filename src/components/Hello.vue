<template>
  <div class="frank">
    <h1>{{ msg }}</h1>
    <input type="text" v-model="coin">
    <button @click="get_coin_usd()">update</button>
    <h1>Coin Name: {{update.name}}</h1>
    <h1>USD Rate: {{update.rate}}</h1>
    <h2>Naira Rate: {{update.rate * 578}}</h2>
    <p>
      For a guide and recipes on how to configure / customize this project,<br>
      check out the
      <a href="https://cli.vuejs.org" target="_blank" rel="noopener">vue-cli documentation</a>.
    </p>
    <h3>Installed CLI Plugins</h3>
    <ul>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-router" target="_blank" rel="noopener">router</a></li>
      <li><a href="https://github.com/vuejs/vue-cli/tree/dev/packages/%40vue/cli-plugin-vuex" target="_blank" rel="noopener">vuex</a></li>
    </ul>
  </div>
</template>


<script>
export default {
  name: 'HelloWorld',
  data() {
    return {
      msg: " Crypto/NGN",
      update: {},
      coin: 'btc'
    }
  },

  methods: {
    get_coin_usd(){
      fetch('https://api.livecoinwatch.com/coins/single', {
        method:'POST',
        headers:{
          "Content-Type": "application/json;charset=UTF-8",
          "x-api-key": "e290e7c5-1642-49b3-a153-5d33632d37f5"
        } ,
        body: JSON.stringify({
          "currency": "USD",
          "code": this.coin.toUpperCase(),
          "meta": true
        })
      }).then( response => response.json())
      .then(json => {
        this.update = json
      })
    }
  },

  mounted() {
    this.get_coin_usd()
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h2 {
  color: blue;
  font-size: 200%;
}
h3 {
  margin: 40px 0 0;
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
.frank{

}
</style>
