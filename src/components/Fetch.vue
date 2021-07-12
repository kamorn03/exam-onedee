<template>
  <div>
    <!-- Fetch -->
    <b-container id="infinite-list">
      <b-row>
        <b-col cols="3" v-for="pokemon in pokemons" v-bind:key="pokemon.id">
          <div v-for="poke in pokemon" v-bind:key="poke.id" class="">
            <b-card
              tag="article"
              style="max-width: 20rem"
              v-if="poke.name"
              class="mt-2"
            >
              <b-card-text>
                {{ poke.name }}
              </b-card-text>
              <img :src="poke.sprites.front_default" alt="front_default_img" />
              <!-- <b-button href="#" variant="primary">Go somewhere</b-button> -->
            </b-card>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import axios from "axios";
export default {
  components: {},
  data() {
    return {
      pokemons: [],
      total: 0,
      next: "",
    };
  },
  mounted() {
    // const axios = require("axios");
    let self = this;
    axios.get("https://pokeapi.co/api/v2/pokemon/").then((response) => {
      response.data.results.forEach((element) => {
        axios.get(element.url).then((poke) => {
          //   console.log(poke);
          //   console.log(poke.data.name);
          if (poke.data.name) {
            self.pokemons.push(poke);
          }
        });
      });
      // next
      console.log(response.data.next);
      if (response.data.next) {
        this.isHasNext(response.data.next);
      }
    });

    window.onscroll = () => {
      let bottomOfWindow =
        Math.floor(document.documentElement.scrollTop + window.innerHeight) ===
        document.documentElement.offsetHeight;

      if (bottomOfWindow) {
        self.isHasNext(self.next);
      }
    };
  },
  methods: {
    isHasNext(url) {
      //   console.log(url);
      let self = this;
      //   console.log(this.next);
      axios.get(url).then((response) => {
        // console.log(response);
        response.data.results.forEach((element) => {
          axios.get(element.url).then((poke) => {
            //   console.log(poke);
            //   console.log(poke.data.name);
            if (poke.data.name) {
              self.pokemons.push(poke);
            }
          });
        });

        this.total = response.data.count;
        this.next = response.data.next;
      });
    },
  },
  name: "Fetch",
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
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
