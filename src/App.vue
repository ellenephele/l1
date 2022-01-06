<template>
  <div id="app">
    <img alt="Calc logo" src="./assets/logo.png">
    <HelloWorld msg="Зачем считать в уме, если у тебя есть я?)"/>
    <Calc/>
  </div>
</template>

<script>
import Calc from './components/Calc';
import HelloWorld from './components/HelloWorld';

export default {
  name: 'App',
  components: {
    HelloWorld,
    Calc,
  },
  data() {
    return {
    };
  },
  methods: {
  },
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #696969;
  margin-top: 60px;
}
</style>
