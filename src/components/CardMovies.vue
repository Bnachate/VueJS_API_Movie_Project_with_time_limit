<template>
  <v-card :loading="loading" class="" max-width="374">
    <template>
      <v-progress-linear color="deep-purple" height="10" indeterminate />
    </template>

    <v-img :src="image" height="250" />

    <v-card-title>{{ title }}</v-card-title>

    <v-card-text>
      <!-- <v-row align="center" class="mx-0">
        <v-rating
          :value="4.5"
          color="amber"
          dense
          half-increments
          readonly
          size="14"
        />

        <div class="grey--text ms-4">4.5 (413)</div>
      </v-row> -->

      <div class="my-4 text-subtitle-1">{{ status }}</div>

      <div>
        <p>{{ synopsis }}</p>
      </div>
    </v-card-text>

    <v-divider class="mx-4" />

    <v-card-title>Genres</v-card-title>

    <v-card-text>
      <v-chip-group
        v-for="(genre, index) in genres"
        :key="index"
        v-model="selection"
        active-class="deep-purple accent-4 white--text"
        style="display: inline"
      >
        <v-chip>{{ genre }}</v-chip>
      </v-chip-group>
    </v-card-text>

    <v-card-actions>
      <v-btn color="deep-purple lighten-2" text>
        <router-link :to="`/about/?id=${id}`"> Show More</router-link>
      </v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  // props: ["title", "synopsis", "status", "genres", "image", "id"],
  props: {
    title: {
      type: String,
      default: '',
    },
    synopsis: {
      type: String,
      default: '',
    },
    status: {
      type: String,
      default: '',
    },
    genres: {
      type: Array,
      default: () => ([]),
    },
    image: {
      type: String,
      default: '',
    },
    id: {
      type: String,
      default: '',
    },
  }
};
</script>
<style scoped>
p {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  max-width: 75ch;
}
</style>