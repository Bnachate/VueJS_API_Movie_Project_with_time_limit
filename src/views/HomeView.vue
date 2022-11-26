<template>
  <v-app>
    <v-main>
      <v-row class="mt-5">
        <!-- le v-for est toujours en debut de balise -->
        <!-- v-bind toujours avant les propriétés qui ne le sont pas -->
        <v-col v-for="anime in animes" :key="anime._id" cols="6" sm="3">
          <CardMovies
            :id="anime._id"
            :title="anime.title"
            :synopsis="anime.synopsis"
            :status="anime.status"
            :genres="anime.genres"
            :image="anime.image"
          />
        </v-col>
      </v-row>
    </v-main>
  </v-app>
</template>

<script>
import axios from "axios";
import CardMovies from "../components/CardMovies.vue";

export default {
  name: "App",
  components: {
    CardMovies,
  },
  data() {
    return {
      animes: [],
    };
  },
  mounted() {
    this.getRequest();
  },
  methods: {
    getRequest() {
      const that = this;
      const options = {
        method: "GET",
        url: "https://anime-db.p.rapidapi.com/anime",
        params: {
          page: "1",
          size: "20",
          sortBy: "ranking",
          sortOrder: "asc",
        },
        headers: {
          "X-RapidAPI-Key":
            "8e2f9c1a4emsh568bd7b8498bd75p181b3djsned9506eac498",
          "X-RapidAPI-Host": "anime-db.p.rapidapi.com",
        },
      };

      axios
        .request(options)
        .then(function (response) {
          that.animes = response.data.data;
          console.log("that.raw", that.animes);
        })
        .catch(function (error) {
          console.error(error);
        });
    },
  },
};
</script>
