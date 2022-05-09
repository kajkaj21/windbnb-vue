<script setup>
import { computed } from "vue";
const props = defineProps({
  rating: Number,
  superHost: Boolean,
  photo: String,
  title: String,
  type: String,
  beds: Number,
  maxGuests: Number,
});

const bedsCount = computed(() => {
  if (props.beds === null) return "0 Beds";
  if (props.beds === 1) return "1 Bed";
  return `${props.beds} Beds`;
});
</script>

<template>
  <div class="container">
    <div class="img-container">
      <img :src="photo" alt="image-of-place" />
    </div>
    <div class="info">
      <div class="about">
        <span v-if="props.superHost" class="super-host">super host</span>
        <p class="overview">
          {{ props.type }}, <span>{{ bedsCount }}</span>
        </p>
      </div>
      <div class="rating">
        <span class="material-icons icon"> star </span>
        <span>{{ props.rating }}</span>
      </div>
    </div>
    <h3>{{ props.title }}</h3>
  </div>
</template>

<style lang="scss" scoped>
.container {
  cursor: pointer;
  font-family: "Montserrat", sans-serif;
  width: 100%;
  max-width: 40rem;

  &:hover {
    img {
      transform: scale(1.2);
    }
  }

  .img-container {
    border-radius: 24px;
    margin-bottom: 1.5rem;
    overflow: hidden;

    img {
      display: block;
      width: 100%;
      height: 24rem;
      object-fit: cover;
      transition: 0.5s ease transform;
    }
  }

  .info {
    display: flex;
    align-items: center;
    justify-content: space-between;
    margin-bottom: 1.2rem;

    .about {
      display: flex;
      align-items: center;

      .super-host {
        font-weight: 700;
        text-transform: uppercase;
        color: #4f4f4f;
        border: solid 1px #4f4f4f;
        border-radius: 12px;
        padding: 0.6rem;
        margin-right: 1rem;
      }

      .overview {
        color: #828282;
      }
    }

    .rating {
      display: flex;
      align-items: center;
      gap: 0.65rem;
      font-size: 1.2rem;
      font-weight: 500;
      color: #4f4f4f;

      .icon {
        font-size: 1.8rem;
        color: rgba(235, 87, 87, 0.72);
      }
    }
  }

  h3 {
    font-weight: 600;
    font-size: 1.4rem;
    color: #333333;
  }
}
</style>
