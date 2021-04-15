<template>

  <div class="w-full flex justify-center">
    <input type="text" placeholder="Enter Pokemon" class="mt-10 p-2 border-blue-500 border-2 ">
  </div>

  <div class="mt-10 p-4 flex flex-wrap justify-center">
    <div class="ml-4 text-xl text-blue-500"
          v-for="(pokemon, idx) in pokemons" :key="idx">
            {{pokemon.name  }}
    </div>
  </div>
</template>

<script>

import {reactive, toRefs} from "vue";

export default {
  name: 'Home',
  setup(){

    const state = reactive({
      pokemons: [],
      urlIdLookup: {}
  
    })

    fetch("https://pokeapi.co/api/v2/pokemon?offset=0")
    .then((res)=> res.json())
    .then((data)=> {
      console.log(data)
      state.pokemons = data.results;
      state.urlIdLookup = data.results.reduce((acc, cur, idx) => 
      acc = { ... acc, [cur.name]:idx+1}

      ,{})
    })

    return {... toRefs(state)}
  }
}
</script>
