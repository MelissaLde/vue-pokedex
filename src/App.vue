<template>
  <main id="app">
    <section class="max-w-xl mx-auto grid gap-10">
      <header class="flex justify-center items-center pt-20">
        <v-search-input v-model="searchFilter" />
      </header>

      <VCardPoke
        v-for="pokemon in filteredPokemon"
        :key="pokemon.name"
        :name="pokemon.name"
        :height="pokemon.height"
        :weight="pokemon.weight"
        :image="pokemon.sprites.front_default"
      />
    </section>
  </main>
</template>

<script>
import VSearchInput from '@/components/VSearchInput'
import VCardPoke from '@/components/VCardPoke'
import { getPokemon, getPokemons } from '@/api/pokeApi'

export default {
  name: 'App',

  components: { VCardPoke, VSearchInput },

  data: () => ({
    searchFilter: '',

    props: {},

    filteredPokemon: [],

    pokemons: [],
  }),

  watch: {
    searchFilter() {
      this.searchPokemon()
    },
  },

  mounted() {
    this.getPokemons()
  },

  methods: {
    searchPokemon() {
      this.filteredPokemon = this.pokemons.filter((pokemon) =>
        pokemon.name.toLowerCase().includes(this.searchFilter.toLowerCase())
      )
    },

    async getPokemons() {
      try {
        const { data } = await getPokemons()

        const pokemonsPromises = data.results.map((pokemon) =>
          getPokemon(pokemon.url)
        )

        const datap = await Promise.all(pokemonsPromises)

        const pokemons = datap.map((pokemon) => pokemon.data)
        this.pokemons = pokemons
        this.filteredPokemon = pokemons

        console.log(datap)
      } catch (error) {
        console.error(error)
      }
    },
  },
}
</script>
