<script>
export default {
    props: [
        'movies','counter'],
    data: () => ({
      show: false,
    }),
}
</script>

<template>
  <v-card
    id="filminfos"
    class="mx-auto"
    v-if="counter < this.movies.length - 1">
<!-- Quelle: Übungsaufgabe 25 -->
  <v-img
    v-if="movies[counter].poster_path.length > 0"
    id="poster"
    :src="'https://www.themoviedb.org/t/p/w300_and_h450_bestv2/' + movies[counter].poster_path"/>
  
  <v-card-title 
    class="text-h4 text-center">{{ movies[counter].title }}
  </v-card-title>
  
  <v-card-actions >
      <v-btn
        color="#F2B705"
        variant="text"
        class="align-center">
        Beschreibung
      </v-btn>
      <v-spacer></v-spacer>
      <v-btn
        :icon="show ? 'mdi-chevron-up' : 'mdi-chevron-down'"
        @click="show = !show"></v-btn>
  </v-card-actions>

  <v-expand-transition>
    <div v-show="show">
      <v-divider></v-divider>
      <v-card-text
        class="text-body-1">{{ movies[counter].overview }}</v-card-text>
    </div>
    </v-expand-transition>
  </v-card>
 
  <v-card v-else>
    <v-card-title >Keine weiteren Filme verfügbar!</v-card-title>   
    <v-alert 
        color="#F2B705"
        density="comfortable"
        variant="elevated"
        icon="mdi-movie-open-remove"
          >Um weitere Filme zu bewerten hol dir jetzt Film-Tinder Premium! (Oder lade die Seite neu...)</v-alert>
    <v-card-text></v-card-text>
  </v-card>
  </template>
  
<style>
  #poster {
    max-height: 50vh;
    margin: auto;
  }
  #filminfos {
    margin-top: 25px
  }
</style>