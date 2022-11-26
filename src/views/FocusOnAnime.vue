<template>
<div style="display: flex; margin: auto; justify-content: center; margin-top: 50px">
  <v-img
    minHeight="300"
    minWidth="600"
    maxWidth="250"
    :src="anime.image"
  ></v-img>
  <v-card class="" max-width="874">
    <v-card-title>{{ anime.title}}</v-card-title>
    <v-card-text>
      <div>
        {{ anime.synopsis}}
      </div>
    </v-card-text>
    <v-divider class="mx-4" />
    <v-card-title>Tonight's availability</v-card-title>
      <v-row align="center" class="mx-0">
        <v-card-text>
          <v-chip-group
            v-for="genre in anime.genres" :key="genre"
            v-model="selection"
            active-class="deep-purple accent-4 white--text"
            column
          >
            <v-chip>{{ genre }}</v-chip>
          </v-chip-group>
        </v-card-text>
      </v-row>
  </v-card>
  </div>
  <div class="about">
    <!-- <ul v-for="data in anime" :key="data._id">
      <li>{{ data }}</li>
    </ul> -->
    <h1>{{ date }}</h1>
  </div>
</template>
<script>
import axios from "axios";
import moment from "moment";

export default {
  data() {
    return {
      anime: [],
      date: "",
    };
  },
  mounted() {
    this.getRequestFocusAnime();
    console.log('anime', this.anime);
    this.test();
  },
  methods: {
    test() {
      setInterval(() => {
        this.date = moment().format("MMMM Do YYYY, h:mm:ss a");
      }, 1000);
    },
    getRequestFocusAnime() {
      // const that = this;
      const paramsQuery = this.$route.query.id;
      const url = "https://anime-db.p.rapidapi.com/anime/by-id/" + paramsQuery;

      axios
        .get(url, {
          headers: {
            "X-RapidAPI-Key":
              "8e2f9c1a4emsh568bd7b8498bd75p181b3djsned9506eac498",
            "X-RapidAPI-Host": "anime-db.p.rapidapi.com",
          },
        })
        .then((response) => {
          console.log(response.data);
          this.anime = response.data;
        })
        .catch(function (error) {
          console.error(error);
        });
    },
  },
};
</script>
