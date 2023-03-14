<template>
  <div class="modal-backdrop">
    <div class="modal-close" @click="close">
      <div class="moda-close-button">X</div>
    </div>
    <div class="modal">
      <div class="modal-header">
        <div class="modal-header-title">Adicionar bolsa</div>
        <div class="modal-header-description">Filtre e adicione as bolsas do seu interesse</div>
      </div>
      <div class="modal-body">
        <div class="modal-body-filter-container">
          <Select class="modal-body-filter-citySelect" label="SELECIONE SUA CIDADE" :options="uniqueCity"
            @input="handleSelectedCity" />
          <Select class="modal-body-filter-courseSelect" label="SELECIONE O CURSO DE SUA PREFERENCIA "
            :options="uniqueCorse" @input="handleSelectedCourse" />
        </div>
        <div class="modal-body-filter-container">
          <div class="modal-body-filter-check-container">
            <label class="modal-body-filter-checkbox-label">Comovo Voce quer estudar?</label>
            <div class="modal-body-filter-checkbox-container">
              <Checkbox @change="handleIsPresencial" class="modal-body-filter-checkbox-shift" description="Presencial">
              </Checkbox>
              <Checkbox @change="handleIsEAD" class="modal-body-filter-checkbox-kind" description="A distancia">
              </Checkbox>
            </div>
          </div>
          <div class="modal-body-filter-slide-container">
            <Slider @input="handleSelectecMaxValue" label="ATE QUANTO PODE PAGAR?" :min="0" :max=10000 :step="50">
            </Slider>
          </div>
        </div>
        <div class="modal-body-offerList-container">
          <div class="modal-body-offerList-filter-container">
            <div class="modal-body-offerList-filter-title">Resultado:</div>
            <div class="modal-body-offerList-filter-select-container">
              <div class="modal-body-offerList-filter-select-title">Ordenar por</div>
              <Select @change="handleselectedOrderingOption" class="modal-body-offerList-filter-select" :options="offerOrderOptions" :isOrderSelect="true"></Select>
            </div>
          </div>
          <div class="modal-body-offerList-list-container" ref="offerList">
            <OfferCard @change="handleCheckMarked" v-for="(Offer, index) in filteredData" :offer="Offer" :key="index" id="offer-card"></OfferCard>
          </div>
        </div>
      </div>
      <div class="modal-footer">
        <button type="button" @click="close" class="modal-footer-bttn-close"> cancelar</button>
        <button type="button" @click="saveOffer" class="modal-footer-bttn-add" :disabled="buttonDisabled"> Adicionar bolsa(s)</button>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  name: "AddCourseModal",
  mounted() {
    this.fetchData();
  },
  methods: {
    close() {
      this.$emit('close')
    },
    handleSelectedCity(event) {
      this.selectedCity = event.target.value
    },
    handleSelectedCourse(event) {
      this.selectedCourse = event.target.value
    },
    handleSelectecMaxValue(event) {
      this.selectedMaxValue = event.target.value
    },
    handleselectedOrderingOption(event) {
      this.selectedOrderingOption = event.target.value
    },
    handleIsEAD(event) {
      this.isEAD = event.target.checked
    },
    handleIsPresencial(event) {
      this.isPresencial = event.target.checked
    },
    fetchData() {
      fetch('db.json')
        .then(response => response.json())
        .then(data => {
          this.offerList = data
        })
    },
    saveOffer() {
      const list = this.$refs.offerList
      const cardList = Array.from(list.querySelectorAll('#offer-card'));
      const selectedCards = cardList.filter(card => {
        return card.firstChild.firstChild.__vueParentComponent.data.isChecked == true
      })
      let newOfferData = selectedCards.map(obj => obj.__vueParentComponent.props.offer.__v_raw)

      if (localStorage.getItem('savedOffer') == null) {
        localStorage.setItem('savedOffer', '[]');
      }

      const savedOffers = JSON.parse(localStorage.getItem('savedOffer'));

      const offersToBeSaved = JSON.stringify(
        newOfferData.reduce((uniqueOffers, offer) => {
          if (!savedOffers.some(savedOffer => JSON.stringify(savedOffer) === JSON.stringify(offer))) {
            uniqueOffers.push(offer);
          }else{
            console.log('Iguais aqui')
          }
          return uniqueOffers;
        }, savedOffers)
      );
      localStorage.setItem('savedOffer', offersToBeSaved);
      this.$emit('close')
      location.reload();
    },
    handleCheckMarked() {
      const list = this.$refs.offerList
      const cardList = Array.from(list.querySelectorAll('#offer-card'));
      const selectedCards = cardList.filter(card => {
        return card.firstChild.firstChild.__vueParentComponent.data.isChecked == true
      })
      this.buttonDisabled = !selectedCards.length > 0;
    }
  },
  components: {
    Select,
    Slider,
    Checkbox,
    OfferCard,
  },
  data() {
    return {
      selectedCity: null,
      selectedCourse: null,
      selectedMaxValue: 10000,
      selectedOrderingOption: null,
      isPresencial: false,
      isEAD: false,
      offerList: [],
      filteredList: [],
      buttonDisabled: true,
      offerOrderOptions:[
        {label: 'Preço', value: 1},
        {label: 'Desconto',value: 2 },
        {label: 'Nome da Faculdade', value:3}
      ]
    }
  },
  computed: {
    uniqueCity() {
      return Object.keys(this.offerList.reduce((types, item) => {
        types[item.campus.city] = true
        return types
      }, {})).map(city => ({ label: city, value: city }))
    },
    uniqueCorse() {
      return Object.keys(this.offerList.reduce((types, item) => {
        types[item.course.name] = true
        return types
      }, {})).map(city => ({ label: city, value: city }))
    },
    filteredData() {
      const filteredOffers = this.offerList.filter(offer => {
        const cityMatch = !this.selectedCity || offer.campus.city === this.selectedCity;
        const courseMatch = !this.selectedCourse || offer.course.name === this.selectedCourse;
        const kindMatch = (!this.isEAD && !this.isPresencial) ||
          (this.isEAD && this.isPresencial) ||
          (this.isEAD && offer.course.kind === 'EaD') ||
          (this.isPresencial && offer.course.kind === 'Presencial');
        const currentValueMatch = (offer.price_with_discount < this.selectedMaxValue);
        return cityMatch && courseMatch && kindMatch && currentValueMatch;
      });
      if(this.selectedOrderingOption == 1) {
        filteredOffers.sort((a, b) => a.price_with_discount - b.price_with_discount);
      }
      if(this.selectedOrderingOption == 2) {
        filteredOffers.sort((a, b) => b.discount_percentage - a.discount_percentage);
      }
      if(this.selectedOrderingOption == 3) {
        filteredOffers.sort((a, b) => a.university.name.localeCompare(b.university.name));
      }
      return filteredOffers;
    },
  }
};


import OfferCard from './OfferCard.vue';
import Checkbox from './utils/Checkbox.vue';
import Select from './utils/Select.vue';
import Slider from './utils/Slider.vue';
</script>
<style>
.modal-backdrop {
  position: fixed;
  inset: 0;
  background-color: rgba(31, 45, 48, 0.88);
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

.modal-close {
  display: flex;
  font-size: 24px;
  background-color: transparent;
  border: none;
  cursor: pointer;
  justify-content: flex-end;
  width: 80%;
  padding: 10px 0%;
  color: white;
  font-weight: bold;
}

.modal-close-button {
  display: flex;
  justify-content: flex-end;
}

.modal {
  background: #FBFBFB;
  box-shadow: 2px 2px 20px 1px;
  overflow-x: auto;
  display: flex;
  flex-direction: column;
  width: 80%;
}


.modal-header {
  display: flex;
  justify-content: flex-start;
  flex-direction: column;
  padding: 3% 5%;

}

.modal-header-title {
  width: 100%;
  font-weight: bold;
  font-size: 30px;
}

.modal-body {
  padding: 0% 5%;
}

.modal-body-filter-container {
  display: flex;
  gap: 2%;
  padding: 15px 0px;
}

.modal-body-filter-citySelect {
  width: 50%;
}

.modal-body-filter-courseSelect {
  width: 50%;
}

.modal-body-filter-check-container {
  width: 50%;
}

.modal-body-filter-slide-container {
  width: 50%;
}

.modal-body-filter-check-container {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  width: 50%;
}


.modal-body-filter-checkbox-container {
  display: flex;
  gap: 10%;
}

.modal-body-offerList-filter-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5% 0;
}

.modal-body-offerList-filter-select-container {
  display: flex;
  align-items: center;
}

.modal-body-offerList-filter-select {
  border: none;
}

.modal-body-offerList-list-container {
  display: flex;
  flex-direction: column;
  gap: 50px;
}

.modal-footer {
  display: flex;
  justify-content: flex-end;
  padding: 3% 5%;
  gap: 2.5%
}

.modal-footer-bttn-close {
  font-weight: bold;
  color: #007A8D;
  border-radius: 5px;
  padding: 1.5% 2.5%;
  border-color: #007A8D;
  background-color: white;
}

.modal-footer-bttn-close:hover{
  color: white;
  background-color: #007A8D;
}

.modal-footer-bttn-add {
  font-weight: bold;
  border-radius: 5px;
  border: none;
  padding: 1.5% 2.5%;
  background-color: #FDCB13;
  white-space: nowrap;
}

.modal-footer-bttn-add:hover {
  background-color: #DE9E1F;
}


.modal-footer-bttn-add:disabled {
  color: rgb(52, 53, 52);
  border-color: rgb(52, 53, 52);
  background-color: gray;
}
</style>