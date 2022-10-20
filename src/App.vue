<template>

  <h1>Hello!</h1>
  <h3>{{ counter }}</h3>
  <button @click="main.oneCount">Count</button>

</template>

<script>
import { useCounterStore } from './store/useCounter';
import { storeToRefs } from "pinia";

export default {
  setup () {
    const main = useCounterStore();
    const { counter, name } = storeToRefs(main);

    return { counter, name }
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
</style>