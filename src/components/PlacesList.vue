<script setup>
import PlaceContainer from "./PlaceContainer.vue";
import { useStore } from "../stores/data.js";

const store = useStore();
</script>

<template>
  <ul>
    <PlaceContainer
      v-for="(stay, id) in store.searchForCurrentFilters"
      :key="id"
      :rating="stay.rating"
      :superHost="stay.superHost"
      :photo="stay.photo"
      :title="stay.title"
      :type="stay.type"
      :beds="stay.beds"
      :maxGuests="stay.maxGuests"
    ></PlaceContainer>
  </ul>
</template>

<style lang="scss" scoped>
ul {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(35rem, 40rem));
  justify-content: center;
  gap: 3.2rem;
}
</style>
