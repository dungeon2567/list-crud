<template>
  <div id="app">
    <div class="divisor">
      <div>
        <ListCrud desc="jogador" plural="jogadores" v-model="jogadores" />
      </div>
      <div>
        <ListCrud desc="time" plural="times" v-model="times" />
      </div>
    </div>
  </div>
</template>
<script>
  import ListCrud from './components/ListCrud'

  export default {
    name: 'App',
    components: {
      ListCrud
    },
    data() {
      return {
        jogadores: [],
        times: []
      }
    }
  }
</script>
<style>

  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }

  .divisor {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 10px;
  }
</style>
