<script setup>
import TheHeader from "./components/TheHeader.vue";
import PlacesList from "./components/PlacesList.vue";
import TheFooter from "./components/TheFooter.vue";
import SearchContainer from "./components/SearchContainer.vue";

import { useStore } from "./stores/data";
import { onBeforeMount } from "vue";

const store = useStore();
onBeforeMount(() => {
  store.currentPlaces = store.stays;
});
</script>

<template>
  <div class="app">
    <SearchContainer
      v-show="store.isSearchboxVisible"
      @closeSearchBox="isSearchboxClicked = false"
    ></SearchContainer>
    <TheHeader
      @showSearchBox="isSearchboxClicked = true"
      class="header"
    ></TheHeader>
    <main>
      <section>
        <div class="current-search-info">
          <h2 v-if="store.selectedLocation === 'Select Location'">
            Stays in Finland
          </h2>
          <h2 v-else>Stays in {{ store.selectedLocation }}</h2>
          <span>{{ store.searchForCurrentFilters.length }} stays</span>
        </div>
        <PlacesList></PlacesList>
      </section>
    </main>
    <TheFooter class="footer"></TheFooter>
  </div>
</template>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@300;400;500;600;700&family=Mulish:wght@300;400;500;600;700&display=swap");

.material-icons {
  font-family: "Material Icons";
  font-weight: normal;
  font-style: normal;
  font-size: 24px; /* Preferred icon size */
  display: inline-block;
  line-height: 1;
  text-transform: none;
  letter-spacing: normal;
  word-wrap: normal;
  white-space: nowrap;
  direction: ltr;

  /* Support for all WebKit browsers. */
  -webkit-font-smoothing: antialiased;
  /* Support for Safari and Chrome. */
  text-rendering: optimizeLegibility;

  /* Support for Firefox. */
  -moz-osx-font-smoothing: grayscale;

  /* Support for IE. */
  font-feature-settings: "liga";
}

* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}

html {
  font-size: 62.5%;
}

.app {
  min-height: 100vh;
  padding: 1.9rem 1.3rem;
  display: flex;
  flex-direction: column;

  @media screen and (min-width: 1290px) {
    padding: 3.2rem 9.6rem;
  }

  .header {
    margin-bottom: 4rem;
  }

  main {
    margin-bottom: 10rem;

    .current-search-info {
      font-family: "Montserrat", sans-serif;
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 2.5rem;

      h2 {
        font-weight: 700;
        font-size: 1.8rem;
        color: #333333;
      }

      span {
        font-weight: 500;
        font-size: 1.4rem;
        color: #4f4f4f;
      }
    }
  }

  .footer {
    margin-top: auto;
  }
}
</style>
