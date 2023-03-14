<template>
  <div class="starrate-container">
        <span>{{ value }}</span>
        <template v-for="i in maxStarNumber" :key="i">
          <font-awesome-icon :icon= 'getStarClass(i)' color="gold" />
        </template>
   </div>
</template>
<script>
export default {
  name:'StarRating',
  props: {
    maxStarNumber: {
      typer: Number,
      default: 5
    },
    value: {
      type: Number,
      default: 3.8
    },
    starIcon: {
      type: String,
      default: 'fa-solid fa-star'
    },
    halfStarIcon: {
      type: String,
      default: 'fa-regular fa-star-half-stroke'
    },
    emptyStarIcon: {
      type: String,
      default: 'fa-regular fa-star'
    },
  },
  methods: {
    getStarClass(index) {
      const value = parseFloat(this.value);
      const full = Number.isInteger(value);
      const ceilValue = Math.ceil(value);
      const isHalfStar = !full && ceilValue === index;
      if (index <= value) {
        return this.starIcon;
      } else if (isHalfStar) {
        return this.halfStarIcon;
      } else {
        return this.emptyStarIcon;
      }
    }
  }
}
</script>
<style>

.starrate-container span {
  margin-right: 20px;
  font-weight: bold;
  font-size: 20px;
}

.font-awesome-icon{
  color: yellow;
}
</style>