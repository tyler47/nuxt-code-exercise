<template>
  <div class="container">
    <section class="section">
      <h1>{{ $route.params.pokemondetail }} JSON Data</h1>
      <vue-json-pretty :data="jsonData"></vue-json-pretty>

    </section>
  </div>
</template>

<script>
export default {
  data() {
    return {
      jsonData: {}
    }
  },
  created () {
    this.getUsers()
  },
  methods: {
    async getUsers() {
      const detailPromise = await fetch(`https://pokeapi.co/api/v2/pokemon/${this.$route.params.pokemondetail?.toLowerCase()}`)
      const detailJson = detailPromise.json()
      detailJson.then((res) => {
       this.jsonData = res;
      })
    }
  }
}
</script>

<style>
h1 {
  font-size: 32px;
}
</style>
