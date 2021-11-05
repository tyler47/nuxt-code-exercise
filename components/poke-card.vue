<template>
  <div class="card">
    <div class="card-image card-image-bg">
      <figure class="image is-4by3 is-flex poke-image is-justify-content-center is-align-content-cente">
        <img
          :src="getPokeSprit(character)"
          alt="Placeholder image"
        />
      </figure>
    </div>
    <div class="card-content">
      <div class="media">
        <div class="media-content">
          <p class="title is-4">{{ pokemonName }}</p>
        </div>
      </div>
      <div>
        <client-only>
          <ul class="m-0" v-if="character">
            <li class="is-size-6 no-bullets"><span class="has-text-weight-bold">Abilities: </span>{{ getAbilities(character) }}</li>
            <li class="is-size-6 no-bullets"><span class="has-text-weight-bold">Types: </span>{{ getTypes(character) }}</li>
            <li class="is-size-6 no-bullets"><span class="has-text-weight-bold">HP: </span>{{ getHp(character) }}</li>
            <li class="is-size-6 no-bullets"><span class="has-text-weight-bold">Attack: </span>{{ getAttack(character) }}</li>
            <li class="is-size-6 no-bullets"><span class="has-text-weight-bold">Defense: </span>{{ getDefense(character) }}</li>
          </ul>
        </client-only>
        <button type="button" class="button learn-more mt-5" @click="$router.push(`/pokemondetail/${pokemonName}`)">
          <span>
            Learn more
          </span>
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "PokeCard",
  props: {
    pokemonName: {type: String, default: ""}
  },
  data: () => ({
    character: {}
  }),
  methods: {
    // @TODO: move to centralized service 
    // get string concat of all abilities 
    getAbilities(character) {
      if (!character.abilities) {
        return '';
      }
      var abilities = character.abilities.map(x => x.ability);
      
      return abilities.map((x) => {
        const abilityName = x.name.replace('-', ' ');
        return abilityName.charAt(0).toUpperCase() + abilityName.slice(1);
      }).join(', ');
    },
    // get string concat of all character types
    getTypes(character) {
      if (!character.types) {
        return '';
      }
      var types = character.types.map(x => x.type);
      
      return types.map((x) => {
        const typeName = x.name.replace('-', ' ');
        return typeName.charAt(0).toUpperCase() + typeName.slice(1);
      }).join(', ');
    },
    // get HP stat from json
    getHp(character) {
      if (!character.stats) {
        return '';
      }
      var stat = character.stats.find(x => x.stat.name === 'hp');
      return stat?.base_stat;
    },
    // get attack stat from json
    getAttack(character) {
      if (!character.stats) {
        return '';
      }
      var stat = character.stats.find(x => x.stat.name === 'attack');
      return stat?.base_stat;
    },
    // get defense stat
    getDefense(character) {
      if (!character.stats) {
        return '';
      }
      var stat = character.stats.find(x => x.stat.name === 'defense');
      return stat?.base_stat;
    },
    // Get Display image for character
    getPokeSprit(character) {
      if (!character.sprites) {
        return '';
      }
      return character.sprites.other['official-artwork'].front_default;
    }
  },
  async fetch() {
    if (!!this.pokemonName) {
      this.character = await this.$http.$get('https://pokeapi.co/api/v2/pokemon/' + this.pokemonName.toLowerCase());
    }
  },
};
</script>

<style>
 .title{
   font-weight: 900;
 }
 .no-bullets {
   list-style-type: none;
   margin:  0;
 }
 .learn-more {
   border-color: #5700ff;
   border-radius: 20px;
   border-width: 2px;
   color: #5700ff;
   font-weight: 600;
   height: 25px;
   padding: 20px 30px;
 }
 .learn-more:hover {
   background: #5700ff;
   border-color: #5700ff;
   color: #FFF;
 }
 .card-image-bg {
   background: #E0E0E0;
 }
 .is-4by3.poke-image img {
   height: auto;
   margin: auto;
   width: 70%;
 }
 .card-content {
   padding: 40px;
 }
 .card-content .media {
   margin-bottom: 10px;
 }
</style>
