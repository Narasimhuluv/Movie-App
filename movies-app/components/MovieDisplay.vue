<template>
  <div>
    <div class="container flex filter__Section">
      <section class="flex justify__between" v-for="btn in buttons" :key="btn">
        <button
          @click="handleFilters(btn)"
          :class="filterName == btn ? 'active' : ''"
        >
          {{ btn }}
        </button>
      </section>
    </div>

    <div class="container flex flex__wrap justify__between popup">
      <span class="flex justify__center items__center" @click="handlePopup">
        <img
          src="https://cdn-icons.flaticon.com/png/512/2997/premium/2997933.png?token=exp=1649744949~hmac=1689c34fcf336dd9698ef11ef71c1f6d"
          alt=""
          class="logo"
        />
      </span>
      <article v-for="(each, index) in data" :key="index" class="flex__23">
        <NuxtLink :to="`${each.id}`">
          <img :v-if="each.image" :src="each.image.medium" alt="" />
        </NuxtLink>
        <p>{{ each.name.slice(0, 50) }}</p>
        <a :href="each.url">tvMaze</a>
        <button @click="handleAdd(each)">Add to Watch</button>
      </article>
    </div>
    <div v-if="popup">
      <Popup
        :popup="popup"
        :handlePopup="handlePopup"
        :favoritedMovies="favoritedMovies"
        :handleAdd="handleAdd"
      />
    </div>
  </div>
</template>

<script>
let AllButtons = ["A-Z", "Runtime", "Rating", "Genres"];
export default {
  name: "NuxtMovieDisplay",
  props: [
    "data",
    "popup",
    "favoritedMovies",
    "handleAdd",
    "filterName",
    "handleFilters",
  ],

  data() {
    return {
      buttons: AllButtons,
    };
  },
  methods: {
    handlePopup(bool) {
      this.popup = bool;
    },
    handleAdd(add, index) {
      this.favoritedMovies = [...this.favoritedMovies, add];
      let formattedWatchedList = JSON.stringify(this.favoritedMovies);
      localStorage.setItem("watchedMovies", formattedWatchedList);
    },
  },
};
</script>

<style scoped>
.placeholder {
  width: 100%;
  display: block;
  height: 60%;
  border-radius: 0.5rem;
  margin-block: 0.5rem;
}
article {
  margin: 1rem 0;
}
span {
  width: 20%;
  height: 200px;
  margin: 2rem 0;
  border-radius: 0.5rem;
}
.logo {
  width: 5rem;
  border: 1px solid gray;
  padding: 1rem;
  border-radius: 50%;
}
p {
  margin: 0.5rem 0;
}
.popup {
  position: relative;
}
button {
  display: block;
  margin-top: 1rem;
}
.filter__Section {
  margin-top: 50px;
  margin-bottom: 20px;
}
.filter__Section button {
  border: none;
  background: none;
  border: 1px solid gray;
  padding: 0.3rem 1.2rem;
  border-radius: 5px;
  margin: 1rem;
}
.active {
  background-color: green;
}
button {
  background: none;
  border: none;
  border: 1px solid gray;
  padding: 0.5rem 0.8rem;
  border-radius: 0.5rem;
}
</style>
