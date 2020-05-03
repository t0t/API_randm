<template>
  <div id="app">
    <h1 class="title">Consultar Datos</h1>
    <button class="button issuccess is-rouded" v-on:click="fetch()">Consultar</button>

    <div class="container">
      <character
        v-for="character of characters"
        v-bind:key="character.id"
        v-bind:character="character"
      />
    </div>
    <nav class="pagination">
      <a class="pagination-previous" v-on:click="changePage(page - 1)">Anterior</a>
      <ul>
        <li class="pagination-link is-current">{{page}}</li>
      </ul>
      <a class="pagination-previous" v-on:click="changePage(page + 1)">Siguiente</a>
    </nav>
  </div>
</template>

<script>
import axios from "axios";
import Character from "@/components/Character";
export default {
  name: "App",
  components: {
    Character
  },
  data: function() {
    return {
      characters: [],
      page: 1,
      pages: 1
    };
  },
  created() {
    this.fetch();
  },
  methods: {
    fetch() {
      const params = {
        page: this.page
      };
      let result = axios
        .get("https://rickandmortyapi.com/api/character/", { params })
        .then(res => {
          this.characters = res.data.results;
          this.pages = res.data.info.pages;
          console.log(res.data);
        })
        .catch(err => {
          console.log(err);
        });
    },
    changePage(page) {
      this.page = page <= 0 || page > this.pages ? this.page : page;
      this.fetch();
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
}
img {
  width: 50px;
}
</style>
