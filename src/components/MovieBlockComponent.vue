<template>
  <div :class="blockClass">
    <img :src="imageUrl" alt="Movie poster">
    <div class="movie-info">
      <h2>{{ movie.title }}</h2>
      <p>{{ movie.overview }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ['movie', 'index', 'sortType'],
  computed: {
    imageUrl() {
      return this.movie.poster_path;
    },
    blockClass() {
      if (this.sortType === 'alternating') {
        return this.index % 2 === 0 ? 'block-normal' : 'block-reverse';
      } else if (this.sortType === 'imageLeft') {
        return 'block-normal';
      }
      return this.index % 2 === 0 ? 'block-normal' : 'block-reverse';
    }
  }
}
</script>

<style scoped>
.block-normal, .block-reverse {
	border: 2px solid black;
  display: flex;
  justify-content: space-around;
  align-items: center;
  width: 1020px;
  height: 324px;
  margin-bottom: 20px;
  background-color: #C4C4C4;
}

.block-normal img,
.block-reverse img {
  width: 380px;
  height: 264px;
}

.block-normal .movie-info,
.block-reverse .movie-info {
  display: flex;
  flex-direction: column;
  justify-content: center;
  width: 269px;
  height: 130px;
  padding: 10px;
}

.block-normal .movie-info {
  margin-left: 20px;
}

.block-reverse .movie-info {
  margin-right: 20px;
}

.block-reverse {
  flex-direction: row-reverse;
}

h2 {
  font-size: 24px;
  margin: 0 0 10px;
}

p {
  margin: 0;
}
@media (max-width: 768px) {
  .block-normal, .block-reverse {
    width: 100%;
    height: auto;
    flex-direction: column;
    align-items: flex-start;
  }

  .block-normal img,
  .block-reverse img {
    width: 100%;
    height: auto;
  }

  .block-normal .movie-info,
  .block-reverse .movie-info {
    width: 100%;
    height: auto;
    margin-left: 0;
    margin-right: 0;
    padding: 20px;
  }

  .block-reverse {
    flex-direction: column;
  }
}

@media (max-width: 480px) {
  h2 {
    font-size: 20px;
  }

  p {
    font-size: 14px;
  }
}
</style>
