<template>
  <div class="lg:ml-16">
    <LandingComp />
    <PopularMoviesComp
      :popularMoviesProp="popularMovies"
      @sendToParent="movieDetails"
    />
    <UpcomingMoviesComp
      :upcomingMoviesProp="upcomingMovies"
      @sendToParent="movieDetails"
    />
    <TopRatedMoviesComp
      :topRatedMoviesProp="topRatedMovies"
      @sendToParent="movieDetails"
    />
  </div>
</template>

<script>
import axios from "axios";
import PopularMoviesComp from "../components/PopularMoviesComp.vue";
import UpcomingMoviesComp from "../components/UpcomingMoviesComp.vue";
import TopRatedMoviesComp from "../components/TopRatedMoviesComp.vue";
import LandingComp from "../components/LandingComp.vue";

export default {
  name: "Home",
  components: {
    PopularMoviesComp,
    UpcomingMoviesComp,
    TopRatedMoviesComp,
    LandingComp,
  },
  data() {
    return {
      popularMovies: null,
      upcomingMovies: null,
      topRatedMovies: null,
    };
  },
  mounted() {
    this.getPopularMovies();
    this.getUpcomingMovies();
    this.getTopRatedMovies();
  },
  methods: {
    getPopularMovies() {
      axios
        .get(
          "https://api.themoviedb.org/3/movie/top_rated?api_key=3f713b362ad34a78305e2fbd42d24840&page=1"
        )
        .then((response) => {
          this.popularMovies = response.data.results.splice(0, 6);
        });
    },
    getUpcomingMovies() {
      axios
        .get(
          "https://api.themoviedb.org/3/movie/upcoming?api_key=3f713b362ad34a78305e2fbd42d24840&language=en-US&page=1"
        )
        .then((response) => {
          this.upcomingMovies = response.data.results.splice(0, 6);
        });
    },
    getTopRatedMovies() {
      axios
        .get(
          "https://api.themoviedb.org/3/movie/top_rated?api_key=3f713b362ad34a78305e2fbd42d24840&language=en-US&page=1"
        )
        .then((response) => {
          this.topRatedMovies = response.data.results.splice(0, 6);
        });
    },
    movieDetails(id) {
      this.$router.push({ path: `movie/${id}` });
    },
  },
};
</script> 
