<script setup>
import { useStore } from "../stores/data.js";

const store = useStore();

const changeLocation = (e) => {
  store.selectedLocation = e.target.closest("li").children[1].innerText;
};
</script>

<template>
  <ul>
    <li
      v-for="location in store.locations"
      :key="location"
      @click="changeLocation($event)"
    >
      <span class="material-icons"> location_on </span>
      <span>{{ location }}</span>
    </li>
  </ul>
</template>

<style lang="scss" scoped>
ul {
  list-style-type: none;
  display: flex;
  flex-direction: column;
  font-family: "Mulish", sans-serif;
  font-weight: 400;
  font-size: 1.4rem;
  color: #4f4f4f;

  li {
    cursor: pointer;
    display: flex;
    align-items: center;
    gap: 1rem;
    padding: 1.8rem;
    border: solid 1px transparent;
    border-radius: 16px;
    transition: 0.3s ease border;

    &:hover {
      border: solid 1px #4f4f4f;
    }
  }
}
</style>
