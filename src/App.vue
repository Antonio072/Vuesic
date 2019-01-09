<template lang="pug">
 #app
  img(src='https://antonio072.github.io/Vuesic/assets/logo.png')
  h1 &#127925 {{ title }} &#127925
  select(v-model="selectedCountry")
    option(v-for="country in countries" 
    v-bind:value="country.value") {{country.name}}
  spinner(v-show="loading")
  ul
   artist(v-for="artist in artists"
          v-bind:artist="artist" v-bind:key="artist.mbid")

</template>

<script>
import Artist from "./components/Artist.vue";
import getArtists from "./api";
import Spinner from "./components/Spinner.vue";
export default {
  name: "app",
  data() {
    return {
      title: " Vue-sic ",
      artists: [],
      countries: [
        { name: "Argentina", value: "argentina" },
        { name: "México", value: "mexico" },
        { name: "España", value: "spain" },
        { name: "Colombia", value: "colombia" },
        { name: "Australia", value: "australia" },
        { name: "Estados Unidos", value: "united states" },
        { name: "Venezuela", value: "venezuela" },
        { name: "Canadá", value: "canada" },
        { name: "Reino Unido", value: "united kingdom" },
      ],
      selectedCountry: "argentina",
      loading: true
    };
  },
  components: {
    Artist,
    Spinner
  },
  methods: {
    refreshList() {
      const self = this;
      this.loading = true;
      this.artists = [];
      getArtists(this.selectedCountry)
        .then(artists => (self.artists = artists))
        .catch(error => console.error(error))
        .finally(() => (self.loading = false));
    }
  },
  mounted() {
    this.refreshList;
  },
  watch: {
    selectedCountry: function() {
      this.refreshList();
    }
  }
};
</script>


<style lang="stylus">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
