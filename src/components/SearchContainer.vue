<script setup>
import CitiesList from "./CitiesList.vue";
import SelectGuestsContainer from "./SelectGuestsContainer.vue";
import { useStore } from "../stores/data";
import { computed } from "vue";
const emits = defineEmits(["closeSearchBox"]);

const store = useStore();
const showGuestsCount = computed(() => {
  if (store.guestsCount === 0) return "Add Guests";
  if (store.guestsCount === 1) return "1 Guest";
  return `${store.guestsCount} Guests`;
});

const changeToGuests = () => (store.showLocation = false);
const changeToLocation = () => (store.showLocation = true);

const selectedGuestsColor = computed(() => {
  return !store.showLocation ? "#333" : "#bdbdbd";
});
const selectedLocationColor = computed(() => {
  return store.showLocation ? "#333" : "#bdbdbd";
});

const isSelected = computed(() => {
  return (
    store.adultsCount !== 0 ||
    store.childrenCount !== 0 ||
    store.selectedLocation !== "Select Location"
  );
});

const searchForCurrentFilters = () => {
  store.isSearchboxVisible = false;
};

const removeSelectedLocation = (e) => {
  const section = document.querySelector("section");
  if (e.target === section) store.selectedLocation = "Select Location";
};

const closeSearchbox = () => {
  store.isSearchboxVisible = false;
};

const reset = () => {
  store.isSearchboxVisible = false;
  store.selectedLocation = "Select Location";
  store.adultsCount = 0;
  store.childrenCount = 0;
};
</script>

<template>
  <section @click="removeSelectedLocation($event)">
    <div class="top">
      <h3>Edit your search</h3>
      <span class="material-icons icon" @click="closeSearchbox"> close </span>
    </div>
    <div class="choices-container">
      <div class="location" @click="changeToLocation">
        <h4>location</h4>
        <span class="selected-location">{{ store.selectedLocation }}</span>
      </div>
      <div class="guests" @click="changeToGuests">
        <h4>Guests</h4>
        <span class="selected-guests">{{ showGuestsCount }}</span>
      </div>
    </div>
    <keep-alive>
      <CitiesList v-if="store.showLocation" class="cities-list"></CitiesList>
      <SelectGuestsContainer
        v-else
        class="guests-container"
      ></SelectGuestsContainer>
    </keep-alive>
    <div class="buttons-container">
      <button @click="searchForCurrentFilters">
        <span class="material-icons"> search </span> Search
      </button>
      <button
        :disabled="!isSelected"
        :class="{ disabled: !isSelected, 'btn-alt': isSelected }"
        @click="reset"
      >
        Clear
      </button>
    </div>
  </section>
</template>

<style lang="scss" scoped>
section {
  z-index: 999;
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  background-color: #fff;
  font-family: "Mulish", sans-serif;
  padding: 1.8rem 2.2rem;
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);

  @media screen and (min-width: 1290px) {
    padding: 9.6rem;
  }

  .top {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 1.6rem;

    h3 {
      font-weight: 700;
      font-size: 1.2rem;
      color: #333333;
    }

    .icon {
      font-size: 1.8rem;
      cursor: pointer;
    }
  }

  .choices-container {
    box-shadow: 0px 1px 6px rgba(0, 0, 0, 0.1);
    border-radius: 16px;
    background-color: #f2f2f2;
    display: flex;
    flex-direction: column;
    gap: 1px;
    overflow: hidden;
    margin-bottom: 3.6rem;

    @media screen and (min-width: 1290px) {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
    }

    & > * {
      background-color: #fff;
      padding: 1rem 2.5rem;
    }

    .location {
      cursor: pointer;
      h4 {
        margin-bottom: 0.3rem;
        text-transform: uppercase;
        color: #333;
      }

      span {
        font-weight: 400;
        font-size: 1.4rem;
        color: v-bind(selectedLocationColor);
      }
    }
    .guests {
      cursor: pointer;
      h4 {
        margin-bottom: 0.3rem;
        text-transform: uppercase;
        color: #333;
      }

      span {
        font-weight: 400;
        font-size: 1.4rem;
        color: v-bind(selectedGuestsColor);
      }
    }
  }

  .cities-list,
  .guests-container {
    margin: 0 3rem;
  }

  .buttons-container {
    display: flex;
    justify-content: flex-end;
    gap: 3.2rem;
    margin-top: 5rem;

    .disabled {
      cursor: default;
      visibility: hidden;
      pointer-events: none;
    }

    .btn-alt {
      cursor: pointer;
      background-color: transparent;
      border: solid 1px rgba(235, 87, 87, 0.9);
      color: rgba(235, 87, 87, 0.9);
    }

    button {
      cursor: pointer;
      font-family: inherit;
      width: 12.5rem;
      height: 5rem;
      border: 0;
      border-radius: 16px;
      background: rgba(235, 87, 87, 0.9);
      color: #f2f2f2;
      box-shadow: 0px 1px 6px rgba(0, 0, 0, 0.1);
      font-size: 1.4rem;
      font-weight: 700;
      display: flex;
      align-items: center;
      justify-content: center;
      gap: 0.5rem;

      span {
        font-size: 2rem;
      }
    }
  }
}
</style>
