<template>
  <div id="app">
    <SliderComponent />
    <ContactForm />
    <div class="sort-options">
    </div>
    <MovieListComponent :movies="sortedMovies" :sortType="sortType" />
  </div>
</template>

<script>
import SliderComponent from './components/SliderComponent.vue';
import ContactForm from './components/ContactFormComponent.vue';
import MovieListComponent from './components/MovieListComponent.vue';
import axios from 'axios';

export default {
  name: 'App',
  components: {
    SliderComponent,
    ContactForm,
    MovieListComponent
},
  data() {
    return {
      movies: [],
      sortType: 'alphabetical',
    };
  },
  computed: {
  sortedMovies() {
    return this.movies.map((movie, index) => ({
      ...movie,
      reverse: this.sortType === 'checkerboard' && index % 2 !== 0
    })).sort((a, b) => {
      if (this.sortType === 'alphabetical') {
        return a.title.localeCompare(b.title);
      }
      return 0;
    });
  }
}
,
  created() {
    axios.get('https://api.themoviedb.org/3/discover/movie?api_key=3685d3eb8695f087227e0ee980f3ae4d&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1')
      .then(response => {
        this.movies = response.data.results.slice(0, 5).map(movie => ({
          title: movie.title,
          description: movie.overview,
          poster_path: `https://image.tmdb.org/t/p/w185_and_h278_bestv2/${movie.poster_path}`
        }));
      })
      .catch(error => {
        console.error('Error fetching movies:', error);
      });
  }
}
</script>

<style>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.sort-options {
  margin-bottom: 20px;
}
</style>
