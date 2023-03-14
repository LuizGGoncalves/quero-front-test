<template>
  <div class="offerCard-container">
    <div class="offer-card-checkbox-container">
      <Checkbox></Checkbox>
      <img :src='offer.university.logo_url' alt="Logo">
      <div class="offer-card-checkbox-description-container">
        <div class="offer-card-checkbox-description-course">{{ offer.course.name }}</div>
        <div class="offer-card-checkbox-description-course-type">{{ offer.course.level }}</div>
      </div>
    </div>
    <div class="offer-card-price-container">
      <div class="offer-card-price-discount">Bolsa de <span>{{ offer.discount_percentage }}%</span></div>
      <div class="offer-card-price-value">R$ {{offer.price_with_discount}}/mes</div>
    </div>
  </div>
</template>
<script>
export default {
  name: "OfferCard",
  props: {
    offer: {
      type: Object,
      required: true
    }
  },
  components: {
    Checkbox
  },
}

import Checkbox from './utils/Checkbox.vue';
</script>
<style>

.offerCard-container{
  display: flex;
  justify-content: space-between;
}

.offer-card-checkbox-container{
  display: flex;
  align-items: center;
  gap: 30px
}

.offer-card-checkbox-container img {
  width: 15%;
}

.offer-card-checkbox-description-container {
  display: flex;
  flex-direction: column;
  height: 100%;
  justify-content:space-between
}

.offer-card-checkbox-description-course {
  color: #007A8D;
  font-weight: bold;
}

.offer-card-price-container{
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-end;
}

.offer-card-price-discount span{
  color: green;
  font-weight: bold;
}

.offer-card-price-value{
  color: green;
  font-weight: bold;
}


</style>