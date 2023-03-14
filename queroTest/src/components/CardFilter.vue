<template>
  <AddCourseModal v-show="isModalVisible" @close="closeModal" />
  <div class="card-filter-container">
    <button :class="{ 'selected': selectedFilter === 'todos' }" @click="selectFilter('todos')">Todos os semestres</button>
    <button :class="{ 'selected': selectedFilter === '2019.2' }" @click="selectFilter('2019.2')">2º semestre de
      2019</button>
    <button :class="{ 'selected': selectedFilter === '2019.1' }" @click="selectFilter('2019.1')">1º semestre de
      2019</button>
  </div>
  <div class="card-list" :class="{ 'card-list--single': filteredOfferCardList.length === 0 }">
    <UserOfferCard @open="showModal" :addNewCard=true></UserOfferCard>
    <UserOfferCard v-for="(Offer, index) in filteredOfferCardList" :key="index" :cardObject="Offer" :addNewCard=false>
    </UserOfferCard>
  </div>
</template>
<script>
export default {
  name: 'CardFilter',
  props: {
    OfferCardList: {
      type: Array,
    },
  },
  data() {
    return {
      selectedFilter: 'todos',
      isModalVisible: false,
    };
  },
  computed: {
    filteredOfferCardList() {
      if (this.selectedFilter == 'todos') {
        return this.OfferCardList;
      } else {
        return this.OfferCardList.filter(offer => offer.enrollment_semester === this.selectedFilter);
      }
    }
  },
  methods: {
    selectFilter(filter) {
      this.selectedFilter = filter;
    },
    showModal() {
      this.isModalVisible = true;
    },
    closeModal() {
      this.isModalVisible = false;
    }
  },
  components: {
    UserOfferCard,
    AddCourseModal
  },
}

import UserOfferCard from "./UserOfferCard.vue"
import AddCourseModal from './AddCourseModal.vue'
</script>
<style>
.card-filter-container {
  display: flex;
  justify-content: flex-end;
  margin-bottom: 2%;
}

.card-filter-container button {
  font-weight: bold;
  color: #007A8D;
  border-radius: 5px;
  padding: 0.5% 2.5%;
  border-color: #007A8D;
  background-color: white;
}

.card-filter-container button.selected {
  background-color: #007A8D;
  color: #fff;
  font-weight: bold;
}

.card-list {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(270px, 1fr));
  grid-auto-rows: 500px;
  gap: 3%;
  grid-row-gap: 20px;
}


.card-list--single {
  grid-template-columns: 300px;
}
</style>