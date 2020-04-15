<template>
  <div>
    <div>
      <v-text-field v-model="queryText" label="Regular"></v-text-field>
      <v-btn rounded block color="primary" @click="handleSearchManga()">Search</v-btn>
    </div>

    <v-divider class="mt-2 mb-2"></v-divider>
    <div>
      <v-row>
        <v-col v-for="manga in results" :key="manga.mal_id" cols="4">
          <v-card class="mt-2" max-width="344" outlined @click="handleMangaClick(manga.url)">
            <v-list-item three-line>
              <v-list-item-content>
                <div class="overline mb-4">
                  <v-icon>mdi-star-half-full</v-icon>
                  {{manga.score}}
                </div>
                <v-list-item-title class="headline mb-1">{{manga.title}}</v-list-item-title>
                <v-list-item-subtitle>{{manga.synopsis}}</v-list-item-subtitle>
              </v-list-item-content>
              <img
                :src="manga.image_url"
                alt
                :style="{width:'80px',marginTop:'10px',marginBottom:'10px'}"
              />
            </v-list-item>
          </v-card>
        </v-col>
      </v-row>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      queryText: "dragon",
      results: []
    };
  },
  methods: {
    handleSearchManga() {
      const url =
        "https://api.jikan.moe/v3/search/manga?q=" + this.queryText + "&page=1";
      axios.get(url).then(response => {
        this.results = response.data.results;
        console.log(this.results);
      });
    },
    handleMangaClick(url){
      window.location = url
    }
  }
};
</script>

<style>
</style>