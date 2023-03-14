<template>
  <div v-if='addNewCard' class="add-card-container">
    <font-awesome-icon icon="fa-solid fa-circle-plus" size="7x" color="#18ACC4" @click="openModal" />
    <div class="add-card-text-container">
      <div class="add-card-title">Adicionar curso</div>
      <div class="add-card-description">Clique para adicionar bolsa de curso do seu interrese</div>
    </div>
  </div>
  <div v-else class="course-card-container">
    <div class="card-university">
      <img :src="cardObject.university.logo_url" alt="Logo">
      <div class="card-university-title">
        <div class="card-university-title-name">{{ cardObject.university.name.toUpperCase() }}</div>
        <div class="card-university-title-course">{{ cardObject.course.name }}</div>
      </div>
      <StarRating class="card-university-starrating" :value="cardObject.university.score"></StarRating>
    </div>
    <div class="card-university-type">
      <div class="card-university-type-kind">{{ cardObject.course.kind.toUpperCase() + '-' +
        cardObject.course.shift.toUpperCase() }} </div>
      <div class="card-university-type-startday">Inicio das aulas em: {{ cardObject.start_date }}</div>
    </div>
    <div class="card-university-value">
      <div class="card-university-value-description">{{cardObject.enabled ? 'Mensalidade com Quero Bolsa:' : 'Bolsa Indisponivel.' }}</div>
      <div v-if="cardObject.enabled" class="card-university-value-oldvalue">R$ {{ cardObject.full_price }}</div>
      <div v-if="cardObject.enabled" class="card-university-value-newvalue">R$ {{ cardObject.price_with_discount }}</div>
      <div v-if="!cardObject.enabled" class="card-university-value-disabled">Entre em contato com o nosso atendimento para saber mais</div>
      <div class="card-univeristy-button">
        <button @click="removeFavOffer" class="card-univeristy-button-delete">Excluir</button>
        <button class="card-univeristy-button-offer" :disabled="!cardObject.enabled">{{cardObject.enabled ? 'Ver oferta' : 'Indisponivel' }}</button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: 'userOfferCard',
  props: {
    addNewCard: {
      type: Boolean,
      requred: true,
    },
    cardObject: {
      type: Object,
    }
  },
  components: {
    StarRating,
  },
  methods: {
    openModal() {
      this.$emit('open')
    },
    removeFavOffer() {
      const savedOffers = JSON.parse(localStorage.getItem('savedOffer'));
      const filteredOffers = savedOffers.filter(offer => JSON.stringify(offer) !== JSON.stringify(this.cardObject));
      console.log(savedOffers)
      console.log(filteredOffers)
      localStorage.setItem('savedOffer', JSON.stringify(filteredOffers));
      location.reload();
    },
  },
}

import StarRating from './StarRating.vue';
</script>
<style>
.add-card-container {
  display: flex;
  box-shadow: rgb(0 0 0 / 24%) 0px 5px 20px;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 15px;
}

.add-card-title {
  margin-top: 20%;
  font-weight: bold;
  font-size: 25px;
  text-align: center;
  padding: 0% 2%;
}

.add-card-description {
  text-align: center;
  padding: 2% 5%;
}

.course-card-container {
  display: flex;
  box-shadow: rgb(0 0 0 / 24%) 0px 5px 20px;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  padding: 15% 0%;
}

.course-card-container img {
  height: 40%;
}

.card-university {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  width: 100%;
}

.card-university img {
  height: 75px;
  max-width: 270px;
}

.card-university-title {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 10%;
}

.card-university-title-name {
  font-weight: bold;
  font-size: 15px;
}

.card-university-title-course {
  font-weight: bold;
  color: #007A8D;
  font-size: 20px;
}

.card-university-starrating {
  margin-top: 5%;
}

.card-university-type {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 10px;
  width: 100%;
}

.card-university-type-kind {
  font-weight: bold;
  font-size: 15px;
}

.card-university-value {
  display: flex;
  flex-direction: column;
  align-items: center;
  width: 100%;
}

.card-university-value-description {
  font-weight: bold;
  margin-bottom: 5%;
}

.card-university-value-oldvalue {
  text-decoration: line-through;
}

.card-university-value-newvalue {
  font-weight: bold;
  font-size: 20px;
  color: green;
}

.card-university-value-disabled{
  text-align: center;
  margin: 0% 10%;
}

.card-university-value-newvalue::after {
  content: ' /mes';
  color: black;
  font-weight: normal;
  font-size: 15px;
}

.card-univeristy-button {
  margin-top: 10%;
  display: flex;
  gap: 10%;
  justify-content: space-around;
}

.card-univeristy-button-delete {
  font-weight: bold;
  color: #007A8D;
  border-radius: 5px;
  padding: 0 15%;
  border-color: #007A8D;
}

.card-univeristy-button-delete:hover {
  color: white;
  background-color: #007A8D;
}

.card-univeristy-button-offer {
  font-weight: bold;
  border-radius: 5px;
  border: none;
  padding: 10% 25%;
  background-color: #FDCB13;
  white-space: nowrap;
}

.card-univeristy-button-offer:hover {
  background-color: #DE9E1F;
}

.card-univeristy-button-offer:disabled {
  color: rgb(52, 53, 52);
  border-color: rgb(52, 53, 52);
  background-color: gray;
}

</style>