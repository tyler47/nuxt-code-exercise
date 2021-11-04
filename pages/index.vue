<template>
  <div class="container">
    <section class="section">
      <h1>Pokemon Cards</h1>
      <h2 class="py-2">Gotta catch ‘em all</h2>
      <div class="columns">
        <div class="column is-one-third">
          <poke-card pokemonName="Charmander"/>
        </div>
        <div class="column is-one-third">
          <poke-card pokemonName="Bulbasaur"/>
        </div>
        <div class="column is-one-third">
          <poke-card pokemonName="Squirtle"/>
        </div>
      </div>
    </section>
  </div>
</template>

<script>
import pokeCard from '../components/poke-card.vue'
export default {
  components: { pokeCard },
}
</script>

<style>
</style>
