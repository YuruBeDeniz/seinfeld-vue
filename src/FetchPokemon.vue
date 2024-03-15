<script>
export default {
  data: () => ({
    pokedex: [1, 2, 3]
  }),
  methods: {
    async fetchPokemon() {
      this.pokedex = await fetch('https://pokeapi.co/api/v2/pokemon?limit=151').then((response) =>
        response.json()
      )
    }
  },
  beforeCreate() {
    console.log('beforeCreate')
    console.log(this.pokedex)
  },
  created() {
    console.log('created')
    console.log(this.pokedex)
    this.fetchPokemon()
  }
}
</script>

<template>
  <h1>Show Pokemons</h1>
  <pre>{{ pokedex }}</pre>
  <button @click="fetchPokemon">Fetch Pokemon</button>
</template>
