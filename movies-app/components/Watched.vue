<template>
  <div class="container">
    <!-- <div v-if="isLoading"></div> -->
    <img v-if="isLoading" src="../assets/images/loading.gif" alt="" />
    <div v-if="!isLoading" class="flex justify__between flex__wrap">
      <article
        :v-if="watchedMovies"
        v-for="(each, index) in watchedMovies"
        :key="index"
        class="flex__23"
      >
        <NuxtLink :to="`${each.id}`">
          <img :v-if="each.image" :src="each.image.medium" alt="" />
        </NuxtLink>
        <p>{{ each.name }}</p>
        <a :href="each.url">tvMaze</a>
      </article>
    </div>
  </div>
</template>

<script>
export default {
  name: "NuxtWatched",
  data() {
    return {
      watchedMovies: [],
      isLoading: true,
    };
  },
  mounted() {
    let data = localStorage.getItem("watchedMovies");
    this.watchedMovies = JSON.parse(data);
    this.isLoading = false;
  },
};
</script>

<style scoped>
article {
  margin: 2rem 0;
}
</style>
