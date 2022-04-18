<!-- Please remove this file from your project -->
<template>
  <div>
    <div class="header__div">
      <Header />
    </div>
    <div v-if="loading">
      <img class="loading__image" src="../assets/images/loading.gif" alt="" />
    </div>
    <div v-else>
      <MovieDisplay
        :data="list"
        :popup="popup"
        :favoritedMovies="favoritedMovies"
        :handleFilters="handleFilters"
        :filterName="filterName"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: "NuxtApp",
  data() {
    return {
      list: [],
      popup: false,
      loading: true,
      favoritedMovies: [],
      filterName: "",
    };
  },
  methods: {
    handleFetch() {
      fetch(`https://api.tvmaze.com/shows`)
        .then((res) => res.json())
        .then((data) => {
          this.list = data;
          this.loading = !this.loading;
        });
    },
    handleFilters(name) {
      this.filterName = name;

      if (name == "A-Z") {
        this.list.sort(function (x, y) {
          let a = x.name.toUpperCase(),
            b = y.name.toUpperCase();
          return a == b ? 0 : a > b ? 1 : -1;
        });
      }
      if (name == "Runtime") {
        this.list.sort((a, b) => {
          return a.runtime - b.runtime;
        });
      }
      if (name == "Rating") {
        this.list.sort((a, b) => {
          return a.rating.average - b.rating.average;
        });
      }
      if (name == "Genres") {
        this.list.sort((x, y) => {
          let a = x.genres[0],
            b = y.genres[0];
          return a == b ? 0 : a > b ? 1 : -1;
        });
      }
    },
  },
  mounted() {
    this.handleFetch();
    // let data = localStorage.getItem("watchedMovies");
    // this.watchedMovies = JSON.parse(data);
  },
  // updated() {
  //   let data = localStorage.getItem("watchedMovies");
  //   this.watchedMovies = JSON.parse(data);
  // },
};
</script>

<style scoped>
.loading__image {
  display: block;
  margin: 150px auto;
  width: 150px;
  height: 150px;
}
.header__div {
  border-bottom: 1px solid rgba(128, 128, 128, 0.26);
}
</style>
