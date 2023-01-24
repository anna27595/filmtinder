<template>
  <v-app>
    <v-app-bar 
      :elevation="10" 
      rounded 
      density="prominent" 
      image="/header2.jpg">
        <template v-slot:image>
          <v-img gradient="to bottom left, rgba(242, 183, 5, 0.2), rgba(242, 183, 5, 1)"></v-img>
        </template>
      <v-app-bar-title>Film-Tinder</v-app-bar-title>
    </v-app-bar>

  <v-main>
    <v-row justify="space-around">
      <v-col cols="12" sm="6" >
        <movieinformation v-bind:movies="movies" v-bind:counter="counter"></movieinformation>
      </v-col>
      <v-col cols="12" sm="4" >
        <v-card id="watchlist">
          <v-card-title >Watchlist</v-card-title>
          <v-list 
            density="comfortable" 
            v-for="title in watchlist"> 
              {{title.title}}
          </v-list>
        </v-card>
      </v-col>
    </v-row>
  </v-main>

  <v-bottom-navigation 
    :elevation="10" 
    bg-color="rgba(242, 183, 5, 0.5)"
    height="60px">
      <addrating @rated="saveRating"></addrating>
      <span><v-btn   
        @click="getMovie"
        prepend-icon="mdi-step-forward"
          > Weiter </v-btn></span>
  </v-bottom-navigation>
</v-app>
</template>

<script>
import movieinformation from './components/movieinformation.vue'
import addrating from './components/addrating.vue'
import axios from 'axios';

export default{
  name: 'app',
  components: {movieinformation, addrating},
  data() {
    return {
        movies: [],
        counter: 0,
        watchlist: []
    }
  },
  methods: {
    getRandomPage() {
//Quelle: https://www.w3schools.com/JS/js_random.asp
        return Math.floor(Math.random() * 500) + 1;
      },
    getMovie() {
        this.counter++;
      },
    saveRating(rating) {
      if (rating==1) {
        this.watchlist.push(
          {title: this.movies[this.counter].title}
          )
        this.getMovie()
          }
      else {this.getMovie()}},},
  mounted() {
//Quelle: Übungsaufgabe 25
    axios
      .get(
        "https://api.themoviedb.org/3/discover/movie?api_key=7619e772e730aa07d69bcd1f3e4da562&language=de-DE&sort_by=popularity.desc&include_adult=false&include_video=false&page=" + this.getRandomPage() + "&with_watch_monetization_types=flatrate"
      )
      .then(response => (this.movies = response.data.results));
  }
}
</script>

<style>
#watchlist {margin-top: 25px; margin-bottom: 60px; padding: 25px}
</style>
