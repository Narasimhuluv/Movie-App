<template>
  <div class="popup container">
    <section class="flex justify__center items__center">
      <img
        @click="handlePopup(false)"
        src="https://cdn-icons.flaticon.com/png/512/2976/premium/2976286.png?token=exp=1649747684~hmac=3d1b33473e6d910af8e7f3978cf88786"
        alt=""
        class="cross"
      />
      <div>
        <form action="" @submit.prevent="handleSubmit" class="form">
          <fieldset>
            <label for="search">Search as your wish</label>
            <input type="text" id="search" v-model="search" />
            <input type="submit" class="submit" />
          </fieldset>
        </form>
      </div>
    </section>

    <section
      class="flex cards__search__sec justify__center items__center flex__wrap"
    >
      <article
        v-for="item in list"
        :key="item.id"
        class="flex__18 searched__article"
      >
        <NuxtLink :to="`${item.show.id}`">
          <img v-if="item.show.image" :src="item.show.image.medium" alt="" />
          <img
            v-else
            src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcS7krJrM4RpWj-YHJOTRhjKNAbldxyFdtAUuA&usqp=CAU"
            alt=""
          />
        </NuxtLink>
        <div class="details__movie">
          <h5>Name : {{ item.show.name }}</h5>
          <p>Language : {{ item.show.language }}</p>
          <button @click="handleAdd(item.show, index)">
            Add to WatchedList
          </button>
        </div>
      </article>
    </section>
  </div>
</template>

<script>
export default {
  name: "NuxtPopup",
  props: ["popup", "handlePopup", "favoritedMovies", "handleAdd"],
  data() {
    return {
      search: "",
      searched: "",
      list: [],
    };
  },
  methods: {
    handleSubmit() {
      this.searched = this.search;
      fetch(`https://api.tvmaze.com/search/shows?q=${this.searched}`)
        .then((res) => res.json())
        .then((data) => {
          this.list = data;
          this.search = "";
          console.log(this.list, "finding clickin");
          this.list.forEach((each) => {
            console.log(each, "each");
          });
        });
    },
  },
};
</script>

<style scoped>
.popup {
  width: 80%;
  height: 95vh;
  position: fixed;
  top: 0%;
  left: 10%;
  background-color: rgba(223, 219, 219, 0.678);
  border-radius: 1rem;
  padding: 2rem 0;
  overflow: auto;
}
.popup::-webkit-scrollbar {
  width: 0;
}
.form {
  position: relative;
  margin: auto;
}
.cross {
  position: absolute;
  top: 2rem;
  right: 2rem;
  width: 2rem;
}
label,
input {
  display: block;
  margin: 0.5rem;
  padding: 0.4rem;
  outline: none;
}
input {
  width: 50rem;
}

.submit {
  width: 8rem;
}
article {
  margin: 2rem;
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  border-radius: 1rem;
  line-height: 1.5;
}
.cards__search__sec {
  width: 100%;
  /* background-color: beige; */
}
.searched__article {
  background-color: rgb(226, 221, 196);
}
.searched__article img {
  width: 100%;
  height: 250px;
  border-radius: 1rem;
}
.details__movie {
  padding: 1rem 0.5rem;
  margin: 0 1rem;
}
button {
  background: none;
  border: none;
  border: 1px solid gray;
  padding: 0.5rem 1rem;
  margin-top: 1rem;
  border-radius: 5px;
}
</style>
