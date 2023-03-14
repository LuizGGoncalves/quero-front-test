<template>
  <Header></Header>
  <NavBar></NavBar>
  <Breadcrumb :items="breadcrumItems" />
  <div class="content">
    <div class="content-title">Bolsas favoritas</div>
    <div class="contetnt-description">Adicione bolsas de cursos e faculdade do seu interesse e recebe atualizações com as
      melores ofertas disponiveis.</div>
    <CardFilter :OfferCardList="favOffer"></CardFilter>
  </div>
  <Footer></Footer>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      breadcrumItems: [
        { text: 'Home', link: '/' },
        { text: 'Minha conta', link: '/produtos' },
        { text: 'Bolsas favoritas', links: '/bolsas-favoritas' }
      ],
    }
  },
  components: {
    Header,
    NavBar,
    Footer,
    Breadcrumb,
    CardFilter,
  },
  computed: {
    favOffer(){
      if (localStorage.getItem('savedOffer') == null) {
        return []
      }else {
        return JSON.parse(localStorage.getItem('savedOffer'))
      }
    }
  }

}

import Header from './components/Header.vue'
import NavBar from './components/NavBar.vue'
import Footer from './components/Footer.vue'
import Breadcrumb from './components/Breadcrumb.vue'
import CardFilter from './components/CardFilter.vue'
</script>

<style>
html {
 height: 100%;
 width: 100%;
}

body {
  height: 100%;
  width: 100%;
  margin: 0;
  background-color: #FBFBFB;
}

#app {
  height: 100%;
  width: 100%;
}

.content {
  padding: 0 5%;
  padding-bottom: 25%;
}

.content-title {
  font-weight: bold;
  font-size: 50px;
}

.contetnt-description {
  padding-top: 10px;
}
</style>
