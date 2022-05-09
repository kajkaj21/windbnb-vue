<script setup>
import { useStore } from "../stores/data";
import { computed } from "vue";

const store = useStore();
const emits = defineEmits(["showSearchBox"]);

const showGuestsCount = computed(() => {
  if (!store.guestsCount) return "Add Guests";
  if (store.guestsCount === 1) return "1 Guest";
  return `${store.guestsCount} Guests`;
});

const selectedGuestsColor = computed(() => {
  return !store.showLocation ? "#333" : "#bdbdbd";
});
const selectedLocationColor = computed(() => {
  return store.showLocation ? "#333" : "#bdbdbd";
});
</script>

<template>
  <header>
    <img src="../assets/logo.svg" alt="logo" />
    <div @click="store.isSearchboxVisible = true" class="search-container">
      <div class="place">{{ store.selectedLocation }}</div>
      <div class="guests">{{ showGuestsCount }}</div>
      <div class="search">
        <span class="material-icons icon"> search </span>
      </div>
    </div>
  </header>
</template>

<style lang="scss" scoped>
header {
  font-family: "Mulish", sans-serif;
  display: flex;
  flex-direction: column;

  @media screen and (min-width: 1290px) {
    flex-direction: row;
    align-items: center;
    justify-content: space-between;
  }

  img {
    align-self: flex-start;
    margin-bottom: 4rem;

    @media screen and (min-width: 1290px) {
      margin: 0;
      align-self: auto;
    }
  }

  .search-container {
    cursor: pointer;
    align-self: center;
    height: 5.5rem;
    width: 100%;
    max-width: 70rem;
    display: grid;
    grid-template-columns: 40% 40% 20%;
    background-color: #fff;
    box-shadow: 0px 1px 6px rgba(0, 0, 0, 0.1);
    border-radius: 16px;
    font-size: 1.4rem;
    font-weight: 400;

    @media screen and (min-width: 1290px) {
      width: 30rem;
    }

    & > * {
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .place {
      border-right: solid 1px #f2f2f2;
      color: v-bind(selectedLocationColor);
    }

    .guests {
      border-right: solid 1px #f2f2f2;
      color: v-bind(selectedGuestsColor);
    }

    .search {
      .icon {
        // font-size: 1.4rem;
        color: rgba(235, 87, 87, 0.9);
      }
    }
  }
}
</style>
