<template>
  <div id="Form">
    <input
      v-model="pokeName"
      class="pokeInput"
      placeholder="Ingrese el nombre de un pokemon"
    />
    <button @click="lookForPokemon()" type="button" class="pokeBtn">
      Buscar
    </button>
    <div>
      <div><img class="pokeImg" :src="pokeImg" />
      </div>
      <h2 class="pokeMovesTitle">Movimientos</h2>
      <div>
        <p
          class="pokeMoves"
          v-for="(pokeMove, $index) in pokeMoves"
          :key="$index"
        >
          {{ pokeMove.move.name }}
        </p>
      </div>
      <h2 class="pokeAbilitiesTitle">Habilidades</h2>
      <div>
        <p
          class="pokeAbilities"
          v-for="(pokeAbility, $index) in abilities"
          :key="$index"
        >
          {{ pokeAbility.ability.name }}
        </p>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Form',
  data: () => ({
    pokeName: 'pikachu',
    poke: ''
  }),

  methods: {
    lookForPokemon() {
      console.log(this.pokeName)
      console.log(this.poke)
      this.lookForPokemonApiRequest()
    },

    lookForPokemonApiRequest() {
      console.log(this.pokeName)
      console.log(this.poke)
      fetch(`https://pokeapi.co/api/v2/pokemon/${this.pokeName}`)
        .then((response) => response.json())
        .then((json) => (this.poke = json))
    }
  },

  computed: {
    pokeMoves() {
      return this.poke.moves
    },
    abilities() {
      return this.poke.abilities
    },
    pokeImg () {
      return (
        this.poke &&
        this.poke.sprites &&
        this.poke.sprites.front_default
      )
    }
  },

  created() {
    return this.lookForPokemon()
  }
}
</script>

<style></style>
