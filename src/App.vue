<template>

  <h1>Hello! from {{ name }}</h1>
  <h3>{{ counter }}</h3>
  <button @click="oneCount">Count</button>
  <button @click="add(10)">Add 10</button>
  <button @click="reset">Reset</button>
  <button @click="randomNum">Random number</button>

</template>

<script>
import { useCounterStore } from './store/useCounter';
import { storeToRefs, mapActions } from "pinia";

export default {
  setup () {
    const main = useCounterStore();

    const { counter, name } = storeToRefs(main);

    // Grabs an action from the store
    const { oneCount } = mapActions(useCounterStore, ["oneCount"]);
    //This works fine as the code above
    // const { oneCount } = main;

    function add(num) {
      //Add changes to state
      main.$patch(() => counter.value += num)
      // This works fine as the code above
      // main.$patch(state => state.counter += num)
    }

    function reset() {
      //resets the state to its original state
      main.$reset()
    }

    //watch for changes in the state
    main.$subscribe((mutation, state) => {
      console.log("mutaion", mutation);
      console.log("state", state);
    })

    function randomNum() {
      // Set state value to something else
      main.$state = {
        counter: Math.floor(Math.random() * 200) 
      }
    }


    return { main, counter, name, oneCount, add, reset, randomNum };
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