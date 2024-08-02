<template>
  <div>
    <RadioButtonsComponent v-model:selectedSort="sortType" />
    <div v-for="(movie, index) in sortedMovies" :key="movie.id">
      <MovieBlockComponent :movie="movie" :index="index" :sortType="sortType" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import RadioButtonsComponent from './RadioButtonsComponent.vue';
import MovieBlockComponent from './MovieBlockComponent.vue';

export default {
  components: { RadioButtonsComponent, MovieBlockComponent },
  data() {
    return {
      movies: [],
      sortType: 'alternating' // По умолчанию шахматный порядок
    };
  },
  computed: {
    sortedMovies() {
      let sorted = [...this.movies];

      if (this.sortType === 'alphabetical') {
        sorted.sort((a, b) => a.title.localeCompare(b.title));
      }

      return sorted;
    }
  },
  created() {
    axios.get('https://api.themoviedb.org/3/discover/movie?api_key=3685d3eb8695f087227e0ee980f3ae4d&language=en-US&sort_by=popularity.desc&include_adult=false&include_video=false&page=1')
      .then(response => {
        this.movies = response.data.results.slice(0, 5).map(movie => ({
          id: movie.id,
          title: movie.title,
          overview: movie.overview,
          poster_path: `https://image.tmdb.org/t/p/w185_and_h278_bestv2/${movie.poster_path}`
        }));
      })
      .catch(error => {
        console.error('Error fetching movies:', error);
      });
  }
}
</script>
