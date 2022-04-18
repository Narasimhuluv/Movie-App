<template>
  <div>
    <div class="container flex justify__center items__center">
      <img
        v-if="isLoading"
        src="../assets/images/loading.gif"
        alt=""
        class="loading"
      />
      <article
        v-else
        v-for="(each, index) in singleMovie"
        :key="index"
        class="flex items__center"
      >
        <img
          :v-if="each.image"
          :src="each.image.original"
          alt=""
          class="mask1 flex__48"
        />
        <div class="flex__48">
          <p class="title">{{ each.name }}</p>
          <span v-for="genre in each.genres" :key="genre" class="genre"
            ><span class="span__genre">{{ genre }}</span
            >,
          </span>
          <p>
            Movie RunTime :
            <span class="span__each">{{ each.runtime }}</span> Min
          </p>
          <p>
            Released Date : <span class="span__each">{{ each.premiered }}</span>
          </p>
          <p>
            Rating : <span class="span__each"> {{ each.rating.average }}</span>
          </p>
          <p>{{ each.summary }}</p>
          <a :href="each.url">tvMaze</a>
          <!-- <button @click="handleAddLocal(each)">Add</button> -->
        </div>
      </article>
    </div>
  </div>
</template>

<script>
export default {
  name: "NuxtSingleMovie",
  data() {
    return {
      singleMovie: [],
      isLoading: true,
      allMovies: [],
    };
  },
  methods: {
    handleFetchSingle() {
      let eachId = this.$route.params.id;
      fetch(`https://api.tvmaze.com/shows/${eachId}`)
        .then((res) => res.json())
        .then((data) => {
          this.singleMovie = [data];
          this.isLoading = false;
          console.log(this.singleMovie, "singleMovie");
        });
    },
    handleAddLocal(add) {
      this.allMovies = [...this.allMovies, add];
      let data = JSON.stringify(this.allMovies);
      localStorage.setItem("watchedMovies", data);
    },
  },
  mounted() {
    this.handleFetchSingle();
  },
};
</script>

<style scoped>
.mask1 {
  width: 100%;
  height: 90vh;
  border-radius: 10px;
  mask-image: linear-gradient(to right, white, transparent);
}
a {
  display: block;
}
.loading {
  width: 100px;
  height: 100px;
}
article {
  width: 100%;
  line-height: 1.5;
}
.title {
  font-weight: bolder;
  font-size: 4rem;
}
.span__genre {
  margin-left: 2rem;
}
.genre {
  margin-left: 3rem;
  margin-bottom: 2rem;
}
.span__each {
  font-weight: bolder;
}
p {
  margin-top: 2rem;
}
</style>
