<script setup>
import { useStore } from "../stores/data.js";

const store = useStore();

const addAdultsCount = () => {
  store.adultsCount++;
};
const subtractAdultsCount = () => {
  if (store.adultsCount === 0) return;
  store.adultsCount--;
};
const addChildrenCount = () => {
  store.childrenCount++;
};
const subtractChildrenCount = () => {
  if (store.childrenCount === 0) return;
  store.childrenCount--;
};
</script>

<template>
  <div class="container">
    <div class="adults">
      <h3>Adults</h3>
      <h4>Ages 13 or above</h4>
      <div class="select-container">
        <button class="minus" @click="subtractAdultsCount">
          <span class="material-icons"> remove </span>
        </button>
        <span class="count">{{ store.adultsCount }}</span>
        <button class="plus" @click="addAdultsCount">
          <span class="material-icons"> add </span>
        </button>
      </div>
    </div>
    <div class="children">
      <h3>Children</h3>
      <h4>Ages 2-12</h4>
      <div class="select-container">
        <button class="minus" @click="subtractChildrenCount">
          <span class="material-icons"> remove </span>
        </button>
        <span class="count">{{ store.childrenCount }}</span>
        <button class="plus" @click="addChildrenCount">
          <span class="material-icons"> add </span>
        </button>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.container {
  font-family: "Mulish", sans-serif;
  display: flex;
  flex-direction: column;
  gap: 5.2rem;

  h3 {
    font-weight: 700;
    font-size: 1.4rem;
    color: #333333;
  }

  h4 {
    font-weight: 400;
    font-size: 1.4rem;
    color: #bdbdbd;
    margin-bottom: 1.2rem;
  }

  .select-container {
    display: flex;
    align-items: center;
    gap: 1.5rem;

    .count {
      font-weight: 700;
      font-size: 1.4rem;
      color: #333333;
    }

    button {
      width: 2.5rem;
      height: 2.5rem;
      border: 1px solid #828282;
      border-radius: 4px;
      background-color: transparent;
      text-align: center;
      color: #828282;
      display: inline-flex;
      align-items: center;
      justify-content: center;

      span {
        font-size: 1.4rem;
      }
    }
  }
}
</style>
