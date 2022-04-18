<template>
  <header class="container flex justify__between items__center">
    <div class="flex">
      <figure class="flex flex__18 items__center">
        <div>
          <img
            v-if="!menuIcon"
            class="menu__icon"
            src="https://cdn-icons.flaticon.com/png/512/6015/premium/6015685.png?token=exp=1649675550~hmac=074b369a586e9cae8210f6d2ee62828d"
            alt="menu icon"
            @click="handleMenu"
          />

          <img
            v-if="menuIcon"
            class="menu__icon"
            src="https://cdn-icons.flaticon.com/png/512/2976/premium/2976286.png?token=exp=1649747684~hmac=3d1b33473e6d910af8e7f3978cf88786"
            alt="menu icon"
            @click="handleMenu"
          />
        </div>
        <div v-if="menuIcon" class="statistics__settings">
          <NuxtLink to="/statistics">
            <p>Statistics</p>
          </NuxtLink>
          <NuxtLink to="/settings">
            <p>settings</p>
          </NuxtLink>
        </div>
        <NuxtLink to="/">
          <lottie-player
            src="https://assets7.lottiefiles.com/datafiles/397tkqLfSbPbfm9/data.json"
            background="transparent"
            speed="1"
            style="width: 50px; height: 50px; margin-left: 2rem"
            loop
            autoplay
          ></lottie-player>
        </NuxtLink>
      </figure>
    </div>
    <nav>
      <NuxtLink to="/watched">
        <p>Added Movies</p>
      </NuxtLink>
    </nav>
  </header>
</template>

<script>
export default {
  name: "NuxtHeader",
  data() {
    return {
      menuIcon: false,
    };
  },
  methods: {
    handleMenu() {
      this.menuIcon = !this.menuIcon;
    },
  },
};
</script>

<style scoped>
header {
  padding: 0.5rem 0;
  position: relative;
}
img {
  display: block;
}
.menu__icon {
  width: 2rem;
  height: 2rem;
}
.menu__logo {
  width: 5rem;
  margin-left: 2rem;
}
.statistics__settings {
  position: absolute;
  top: 6rem;
  padding: 2rem 1rem;
  padding-right: 2rem;
  z-index: 9999;
  background-color: #fff;
}
.statistics__settings p {
  margin-top: 1rem;
}
</style>
